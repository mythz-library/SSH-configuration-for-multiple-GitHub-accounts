# SSH Configuration for Multiple GitHub Accounts

## About SSH

SSH (Secure Shell) is a cryptographic network protocol used to securely connect to and manage remote servers over an unsecured network. It enables secure access to a remote machine for tasks such as command execution, file transfers, and system administration.

<br/>

## Step 01: Open Powershell

<br/>

## Step 02: Move to SSH directory

```sh
 cd ~/.ssh
```

## Step 03: Generating SSH keys

```sh
ssh-keygen -t ed25519 -C "sample@gmail.com"

```

- Next, prompt will ask --> **"Enter file in which to save the key"**, give the file path to .ssh directory + file name for the ssh key. For example, `~/.ssh/id_private`
- Note that: File name must be prefixed by `id_`.
- If I already in the .ssh directory, file name should be `id_private`. No need to mention the path to .ssh dir.
- This will generate the private key as `~/.ssh/id_{file-name}` and the public key as `~/.ssh/id_{file-name}.pub`
- Define the email in key generation command is not mandatory. We can remove it, `ssh-keygen -t rsa -b 4096` enough.

```sh
# Keys for legacy system that does not support Ed25519 algorithm
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

<br/>

## Step 04: Add & Delete ssh keys to the ssh agent

```sh
# List all the existing keys in the ssh agent
ssh-add -l

# Delete all the existing ssh keys in the ssh agent
ssh-add -D

# Adding keys to agent
ssh-add ~/.ssh/id_private
ssh-add ./id_private         # If we're already inside the .ssh dir
```

- Sometimes adding key to the agent is unnecessary. Do this step if the cloning a repo or pushing changes not working as we expected.

<br/>

## Step 05: Create the "config" file & Define the Configurations

This "config" file doesn't have an extention.

```sh
# Example 01
Host github.com
HostName github.com
IdentityFile ~/.ssh/id_rsa
User ashenJay07

# Example 02
Host github.com-library
HostName github.com
IdentityFile ~/.ssh/id_rsa_library
User mythz-library

# Example 03
Host work.github.com
HostName github.com
IdentityFile ~/.ssh/id_work
User ashenwork
```

<br/>

## Step 06: Get the Public Key & Configure it on GitHub

```sh
cat .\id_rsa.pub
```

<br/>

## Step 07: Clone the repository using GitHub SSH URL

```sh
git clone git@<Host>:<GitHub_Username>/<Repo_Name>.git
```

```sh
# Example
git clone git@github-library:mythz-library/SSH-configuration-for-multiple-GitHub-accounts.git
```

<br/>

## Step 08: Update the remote repo URL of an existing repo

- If we're already cloned the repo. We must update the host of remote repo.

```sh
# Step 01: Open the config file
git config -e

# Step 02: Update the host of URL according to our custom configurations (github.com --> github.com-library)
[remote "origin"]
	url = git@github.com-library:mythz-library/SSH-configuration-for-multiple-GitHub-accounts.git
	fetch = +refs/heads/*:refs/remotes/origin/*

```
