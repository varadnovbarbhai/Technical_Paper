## Secure Shell 

Secure Shell is used for seamless transmission of your data from your local Computer to a Cloud Storage Platform like GitLab.

It generates 2 keys namely Private and Public 

The public key is added to the cloud storage platform so that the project that you have built on your local device can be made available on the cloud platform 
for further sharing, manipulation, or collaboration purposes 

A private key is also generated, and it is suggested that the private key not be shared with anyone.

A person accessing your computer can only have access to the private key 

# Secure Shell (SSH)

## Introduction

SSH (Secure Shell) is a network protocol used to establish a secure and encrypted connection between two computers over an unsecured network. It allows users to remotely access, control, and manage computers or servers using a command-line interface.

SSH protects communication by encrypting the data exchanged between the client and the remote server. This prevents unauthorised users from intercepting sensitive information, such as login credentials and commands.

## How SSH Works

SSH works on a client-server model. The client is the computer from which a user initiates a connection, while the server is the remote computer being accessed.

The basic process involves the following steps:

1. **Connection Establishment:** The SSH client connects to the remote server, usually through port 22.
2. **Server Authentication:** The client verifies the identity of the server using its host key.
3. **User Authentication:** The user proves their identity using a password or an SSH key pair.
4. **Encrypted Communication:** Once authentication is successful, an encrypted connection is established.
5. **Remote Operations:** The user can execute commands, manage files, and perform other operations on the remote system.

## SSH Authentication Methods

SSH supports different authentication methods:

- **Password Authentication:** Users enter their username and password to access the remote server.
- **Public Key Authentication:** SSH uses a pair of cryptographic keys: a public key and a private key. The public key is stored on the server, while the private key remains securely on the user's computer.
- **SSH Agent:** An SSH agent securely manages private keys and helps users authenticate without repeatedly entering their key passphrases.

Public key authentication is commonly preferred because it provides a secure and convenient way to access remote systems.

## Uses of SSH

- **Remote Server Access:** Developers and system administrators use SSH to connect to remote servers and execute commands.
- **Secure File Transfer:** SSH supports secure file transfers using SCP and SFTP.
- **Git Authentication:** Developers use SSH keys to connect to GitHub and GitLab repositories securely without entering their account passwords for every operation.
- **Server Administration:** SSH allows administrators to install software, configure services, monitor system performance, and troubleshoot remote machines.
- **Port Forwarding:** SSH can securely forward network traffic from one computer to another.
- **Automation:** SSH can be used in scripts to execute commands and manage multiple remote systems automatically.

## Advantages of SSH

- **Security:** Encrypts communication between the client and server.
- **Authentication:** Supports password-based and public key-based authentication.
- **Remote Accessibility:** Allows users to manage systems from different locations.
- **Data Integrity:** Helps protect transmitted data from unauthorised modification.
- **Automation:** Supports remote command execution through scripts.
- **Efficiency:** Provides secure access through a lightweight command-line interface.

## Common SSH Commands

| Command | Description |
|---|---|
| `ssh username@hostname` | Connect to a remote server. |
| `ssh-keygen` | Generate an SSH key pair. |
| `ssh-add` | Add a private key to the SSH agent. |
| `ssh -T git@gitlab.com` | Test SSH authentication with GitLab. |
| `scp file.txt username@hostname:/path/` | Securely copy a file to a remote server. |

SH Security Best Practices
- Never share your private SSH key with anyone.
- Protect private keys using a strong passphrase.
- Use appropriate file permissions for SSH keys.
- Remove access for SSH keys that are no longer required.
- Verify the server's host key before trusting a new connection.
- Prefer modern algorithms such as Ed25519.
- Disable password authentication on servers when key-based authentication is properly configured and appropriate.

## Conclusion

SSH is an essential protocol for secure remote communication and system administration. It enables developers and administrators to access remote servers, transfer files, automate tasks, and authenticate with Git hosting platforms such as GitHub and GitLab. By providing encryption and secure authentication mechanisms, SSH helps protect sensitive information during network communication.

## References

- OpenSSH – Official Documentation
- GitLab – Use SSH keys to communicate with GitLab
- GitHub – About SSH
