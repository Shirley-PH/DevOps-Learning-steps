# :card_index_dividers:GIT commands

A beginner-friendly guide to the most common Git commands for managing local and remote repositories

## 🖥️Local Repository

1. Configure your Git username and email

Set the username and email address that Git will use when creating commits.
```bash
git config --global user.name "your name"
git config --global user.email "mail@example.com"  
```
2. Create a directory

Create a new directory for your project:
```bash
mkdir my-project  
```
Navigate into the directory:
```bash
cd my-project  
```
3. Initialize the repository

Initialize the directory as a Git repository:
```bash
git init  
```
4. Create README.MD file

Create a README file:
```bash
touch README.md 
```
Add the file to the staging area:
```bash
git add README.md #Staging
```
Save your changes by creating a commit:
```bash
git commit -m "Initial commit"
```
## 🌐Remote Repository Conexion
1. Create a Remote repository

Create a repository on a Git hosting platform, such as:
- Github
- Bitbucket
- Codecommit

2. Clone a remote repository

Download a remote repository to your local machine:
```bash
git clone <repository-URL> #clona the repository from github
```
Example:
```bash
git clone https://github.com/username/repository-name.git #clona the repository from github
```
3. Connect a local repository to a remote repository

If you already have a local repository and want to connect it to a remote repository, use:
```bash
git remote add origin
```
Example using SSH
```bash
ssh://git@github.com/[username]/[repository-name].git #git@github.com:Shirley-PH/DevOps-Learning-steps.git
```
Verify the remote conecction:
```bash
verify remote -v
```

## ⏫ Push and Pull Changes

1. Check your local changes

To check the current state of your working directory and staging area:
```bash
git status
```
2. Add modified files to the staging area

To stage a specific file:
```bash
git add fileName
```
To stage all modified and untracked files in the current directory:
```bash
git add .
```
3. Commit your changes

Create a commit with a descriptive message:
```bash
git commit -m "add your comment"
```

4. Upload local changes to the remote repository

Push your local commits to the remote repository:
```bash
git push origin branchName
```

For the first push of a new branch, you can use:
```bash
git push -u origin branchName
```

Nota: The `-u` option sets the upstream branch, so you can use git push and git pull without specifying the remote and branch every time.

5. Download changes from the remote repository

Download and integrate the latest changes from the remote repository:
```bash
git pull
```
You can also specify the remote and branch:
```bash
git pull origin branchName
```
##  :arrows_clockwise:Branches

1. Create a new branch

Create a new branch without switching to it:
```bash
git branch exampleBranch
```
Alternatively, create a new branch and switch to it immediately:
```bash
git switch -c exampleBranch
```
2. List available branches

To list local branches
```bash
git branch
```
To list both local and remote branches:
```bash
git branch -a
```
3. Switch to another branch

Switch to an existing branch
```bash
git switch exampleBranch
```
Alternatively, you can use:
```bash
git checkout exampleBranch
```
Publish the new branch
```bash
git push -u origin exampleBranch
```
## :man_factory_worker:Troubleshooting

1. Remove a remote connection

If you have connected a local repository to a remote repository and want to remove that connection, use:

```bash
git remote remove origin
```
This removes the remote reference from your local repository. It does not delete the remote repository from GitHub or another hosting platform.

2. Check the remote repository configuration

To verify whether a remote connection has been configured, run:
```bash
git remote -v
```
You should see something similar to:
```bash
origin  https://github.com/username/repository-name.git (fetch)
origin  https://github.com/username/repository-name.git (push)
```
You can also inspect the GIT configuration file:

```bash
cat .git/config 
```
Example output:

```bash
[core]
        repositoryformatversion = 0
        filemode = false
        bare = false
        logallrefupdates = true
        symlinks = false
        ignorecase = true
[remote "origin"]
        url = https://github.com/Shirley-PH/testUpProject.git
        fetch = +refs/heads/*:refs/remotes/origin/*

```

If the `[remote "origin"]` section is missing, it means that no remote named origin is configured.

You can try: `git init` again.
Or
try again:
```bash
git remote add origin <repository-URL>
```

3. Error: src refsec main does not match any

Sometimes, you might encounter the following error when trying to push your changes:
```bash
 error src refspec main does not match any and 
 error: failed to push some refs to '<Repository-URL>'
```
This error commonly occurs when:

- You haven't created your first commit yet.
- The local branch name does not match the branch name you are trying to push.

**Solution 1: Make your first commit**

If you haven't committed any files yet, run:
This happens becouse you have files that is not saved yet. So you only need to run:
```bash
 git add . 
 [result]
 git commit -m "Initial commmit"
 #Then
 git push -u origin main
```

**Solution 2: Check your current branch**

Check which branch you are currently using:
```bash
 git branch
```
If your branch is named master instead of main, you can either push using:
```bash
 git push -u origin master
```
Or rename your current branch to main:
```bash
 git branch -M main
 git push -u origin main
```