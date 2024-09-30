# 2420 assignment 1

This guide aims to guide you through the steps of creating a remote server using DigitalOcean and setting up an Arch Linux Droplet using ```cloud-init```.

Topics the guide will cover:
- Creating ssh keys and add them to your DigitalOcean account
- Adding a custom Arch Linux image
- Creating a droplet running Arch Linux
- Connecting to your droplet from your local machine using SSH
- Using cloud-init to:
    - Create a new regular user
    - Install some initial packages
    - Add a public SSH key to the authorized_keys file in your new user home directory
    - Disable root access via SSH


## Creating ssh keys and add them to your DigitalOcean account
The Secure Shell (SSH) protocol is a method you can use to securely transfer messages to a computer across an unsecured network. Furthermore, this method uses cryptography to verify identities and encrypts communication between your devices.

To create your ssh key:
1. Open your Terminal

2. Paste in the following command in your terminal:
```
ssh-keygen -t ed25519 -f ~/.ssh/<key name> -C <youremail@email.com>
```
![image](https://github.com/user-attachments/assets/e9dd9126-29f9-4b05-8f78-1d291cac7c49)
