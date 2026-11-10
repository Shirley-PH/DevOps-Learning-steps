# Running Apache Tomcat 10 with systemd

This guide demonstrates two ways to run Apache Tomcat 10 on a CentOS/RHEL-style Linux server:

1. Start it manually with Tomcat's scripts for a quick test.
2. Run it as a `systemd` service for consistent, system-managed operation.

The second approach is closer to how an application server is operated in a DevOps environment.

---

## Why systemd and Tomcat matter in DevOps

Tomcat is a Java application server and servlet container. It runs Java web applications and commonly listens for HTTP traffic on port `8080`. Knowing how to deploy and operate Tomcat helps a DevOps engineer support applications between development and production.

`systemd` is the service manager used by many Linux distributions. It starts services, tracks their state, starts configured services during boot, and provides a consistent interface for operations and troubleshooting.

Together, they let an operator:

- Start, stop, restart, and inspect Tomcat consistently with `systemctl`.
- Configure Tomcat to start automatically after a reboot.
- Check service logs and status when diagnosing an outage.
- Run the application under a dedicated, unprivileged Linux account.
- Replace one-off manual steps with a repeatable service configuration that can later be automated with configuration-management or deployment tools.

This is useful operational knowledge for a DevOps role: it connects application deployment with Linux administration, service reliability, security, and troubleshooting.

> **Note:** In this guide, "automatic" means systemd manages the service and can start it at boot. Downloading and installing Tomcat are still manual steps; automating the full installation and deployment would be a separate step, for example with Ansible or a CI/CD pipeline.

---

## Prerequisites

- A CentOS/RHEL-compatible Linux server with administrative (`sudo`) access.
- A supported Java version for the Tomcat 10 release you choose. This example installs OpenJDK 17; check the [Tomcat 10 documentation](https://tomcat.apache.org/tomcat-10.1-doc/) for the requirements of your selected release.
- `curl` or `wget`, and `tar`.

### Step 1: Install Java

```bash
sudo dnf install -y java-17-openjdk
java -version
```

### Step 2: Download Tomcat

Download a current, supported Tomcat 10 release from the [official Apache Tomcat download page](https://tomcat.apache.org/download-10.cgi). Choose a patched release and verify its published checksum or signature, especially outside a learning environment.

Set `TOMCAT_VERSION` to the version you selected (e.g 10.1.24). 

```bash
TOMCAT_VERSION=10.1.24
curl -fLO "https://dlcdn.apache.org/tomcat/tomcat-10/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz"
tar -xzf "apache-tomcat-${TOMCAT_VERSION}.tar.gz"
```

## Option 1: Start Tomcat manually

This is a simple way to confirm that Java and Tomcat run. It is useful for learning or a temporary test, but it does not configure Tomcat to start at boot or let systemd manage its lifecycle.

Run Tomcat as a regular, non-root user; do not start it as `root`.

> ⚠️**Security Best Practice**: Always run Tomcat as a regular, non-root user. Never start production services as root.

From the directory where you extracted Tomcat:

```bash
cd "apache-tomcat-${TOMCAT_VERSION}/bin"
./startup.sh
```

The script should report `Tomcat started`. Confirm that Tomcat responds locally:

```bash
curl -I http://localhost:8080/
```

If you are testing from another machine, the server's firewall and network rules must allow access to port `8080`. Do not expose the port publicly unless that is intended and appropriately secured.

Stop the manually started instance before setting up the systemd service:

```bash
./shutdown.sh
```

## Option 2: Run Tomcat as a systemd service

This setup installs Tomcat under `/opt/tomcat`, runs it as a dedicated `tomcat` account, and lets systemd manage the foreground Tomcat process.

### 1. Create a service account and install Tomcat

Run these commands from the directory containing the extracted Tomcat directory:

```bash
sudo useradd --system --home-dir /opt/tomcat --shell /sbin/nologin --user-group tomcat
sudo mkdir -p /opt/tomcat
sudo cp -a "apache-tomcat-${TOMCAT_VERSION}/." /opt/tomcat/
sudo chown -R tomcat:tomcat /opt/tomcat
```

Giving the service its own account limits the impact of a security vulnerability compared with running it as root.

### 2. Find the Java installation path

systemd does not load an interactive shell profile, so set `JAVA_HOME` explicitly in the service file. Find the path for the Java installation:

```bash
readlink -f "$(command -v java)"
```

For example, if the result is `/usr/lib/jvm/java-17-openjdk-.../bin/java`, set `JAVA_HOME` to the corresponding Java directory, without `/bin/java` at the end. Use the actual path from your server.

### 3. Create the systemd unit

Create `/etc/systemd/system/tomcat.service`:

```bash
sudo tee /etc/systemd/system/tomcat.service > /dev/null <<'EOF'
[Unit]
Description=Apache Tomcat 10
After=network.target

[Service]
Type=simple
User=tomcat
Group=tomcat

WorkingDirectory=/opt/tomcat

Environment="JAVA_HOME=/usr/lib/jvm/java-17-openjdk"
Environment="CATALINA_HOME=/opt/tomcat"
Environment="CATALINA_BASE=/opt/tomcat"

ExecStart=/opt/tomcat/bin/catalina.sh run
ExecStop=/opt/tomcat/bin/catalina.sh stop

Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
EOF
```

Update the `JAVA_HOME` value to the Java directory found in the previous step. `catalina.sh run` keeps Tomcat in the foreground, allowing systemd to track the process directly.

### 4. Load and start the service

After adding or changing a unit file, tell systemd to reload its configuration, then enable and start Tomcat:

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now tomcat
sudo systemctl status tomcat
```

- `enable` configures the service to start during boot; 
- `--now` starts it immediately. Confirm that it responds:

```bash
curl -I http://localhost:8080/
```

### 5. Operate and troubleshoot the service

```bash
sudo systemctl stop tomcat
sudo systemctl start tomcat
sudo systemctl restart tomcat
sudo systemctl status tomcat
sudo journalctl -u tomcat
```

Use `journalctl -u tomcat -f` to follow the service logs while troubleshooting. Tomcat also writes application and server logs under `/opt/tomcat/logs`.

## Manual start vs. systemd-managed service

| Approach | Best for | Starts on boot | Managed with `systemctl` |
|---|---|---:|---:|
| Tomcat `startup.sh` / `shutdown.sh` | Learning and quick tests | No | No |
| systemd unit | Repeatable server operation | Yes, when enabled | Yes |


<FollowUp label="Want me to show you how to configure a firewall rule or set up Nginx as a reverse proxy for Tomcat?" query="How do I configure firewalld to allow port 8080 or set up Nginx as a reverse proxy for Tomcat 10?"/>
