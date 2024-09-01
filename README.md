# SSH Configuration for Multiple GitHub Accounts

## About SSH

SSH (Secure Shell) is a cryptographic network protocol used to securely connect to and manage remote servers over an unsecured network. It enables secure access to a remote machine for tasks such as command execution, file transfers, and system administration.

<br/>

## Step 01: Open Powershell

## Step 02: Move to SSH directory

```sh
 cd ~/.ssh
```

## Step 03: Generating SSH keys

```sh
ssh-keygen -t ed25519 -C "sample@gmail.com" -f ~/.ssh/custom_key_name

```

- `-f ~/.ssh/custom_key_name` specifies the path and name for the SSH key file. Replace `custom_key_name` with your desired file name
- This will generate the private key as `~/.ssh/custom_key_name` and the public key as `~/.ssh/custom_key_name.pub`

```sh
# Keys for legacy system that does not support Ed25519 algorithm
ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f ~/.ssh/custom_key_name
```

## Step 04: Create the "config" file & Define the Configurations

```txt
Host github
HostName github.com
IdentityFile ~/.ssh/id_rsa
User ashenJay07

Host github-library
HostName github.com
IdentityFile ~/.ssh/id_rsa_library
User mythz-library
```

## Step 05: Get the Public Key & Configure it on GitHub

```sh
cat .\id_rsa.pub
```

## Step 06: Clone the repository using GitHub SSH URL

```sh
git clone git@<Host>:<GitHub_Username>/<Repo_Name>.git
```

```sh
# Example
git clone git@github-library:mythz-library/SSH-configuration-for-multiple-GitHub-accounts.git
```
