# AWS Command Line

This section documents my learning journey with the AWS Command Line Interface
(AWS CLI). It explains how to configure AWS credentials and run basic AWS CLI
commands from Git Bash.

## Prerequisites

Before getting started, make sure you have:

- An active AWS account
- The AWS CLI installed
- An IAM user or IAM role with the required permissions
- Git Bash or another terminal

## Creating IAM credentials

In the AWS Management Console, create an IAM user and configure the required
permissions. Use an IAM role where possible, especially when working in AWS
itself or in a shared environment.

For local use, create access keys for the IAM user and store them securely.

> **Security note:** Never share access keys, upload them to GitHub or another
> platform, or commit them to a repository. Anyone with your access keys can use
> them to access AWS resources.

## Configuring the AWS CLI

For this example, use the following configuration:

- **Region:** `us-east-1`
- **Output format:** `json`

Run the configuration command:

```bash
aws configure
```

Enter the following values when prompted:

```text
AWS Access Key ID: <YOUR_ACCESS_KEY_ID>
AWS Secret Access Key: <YOUR_SECRET_ACCESS_KEY>
Default region name: us-east-1
Default output format: json
```

The AWS CLI stores the configuration in the following files:

```bash
ls ~/.aws
cat ~/.aws/config
cat ~/.aws/credentials
```

If you use temporary credentials, such as credentials obtained through AWS
STS or AWS IAM Identity Center, do not add a permanent access key to
`~/.aws/credentials`.

## Verifying the configuration

Check the identity associated with the active credentials:

```bash
aws sts get-caller-identity
```

The command returns the AWS account ID, IAM ARN, and user ID in JSON format.

## Listing EC2 instances

List the EC2 instances in the configured region:

```bash
aws ec2 describe-instances
```

The response contains instance details in JSON format, including instance IDs,
states, addresses, and tags.

## Additional resources

- [AWS CLI documentation](https://docs.aws.amazon.com/cli/latest/)
- [AWS CLI command reference](https://docs.aws.amazon.com/cli/latest/reference/)
