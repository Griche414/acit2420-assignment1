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

1. Open your Linux terminal
    - Ensure you have a ssh directory, if not, create one using this command:
    ```mkdir -p ~/.ssh```
    this command will create a .ssh directory in your home directory, and ```-p``` ensures that no error occurs if the directory already exists.
2. Paste the following command in your terminal:
```
ssh-keygen -t ed25519 -f ~/.ssh/do-key -C "your email address"
```
```ssh-keygen``` is a command that creates your ssh key.
```-t ed25519``` is the type of key created and in this case, it is using the ```ed25519``` algorithm.
```-f``` specifies name of the file and file type.
```~``` is your current home directory
```-C``` allows you to add a comment. Comment can be anything.
3. You may type a passphrase of your choice to provide extra security for your SSH key. It is optional.
A successful SSH key generation looks like this:
![image](https://github.com/user-attachments/assets/e9dd9126-29f9-4b05-8f78-1d291cac7c49)
You have succesfully generated your SSH key.
Note: The command will generate a private and a public key. The private key is saved as ```do-key``` and the public key will be saved as ```do-key.pub```.

Now that you have generated your SSH key, it is time to add them to your DigitalOcean account.
First, we need to copy the content of your SSH keys. To do so, use command:
```Get-Content C:\Users\your-user-name\.ssh\do-key.pub | Set-Clipboard```
This will copy the content of your public key content.

Next, to add the SSH Public Key to your DigitalOcean account:

1.Log into your DigitalOcean account.


2.Click on settings on the left sidebar of your screen. 

![image](https://github.com/Griche414/acit2420-assignment1/blob/main/Assets/image1.png)


3.Click on Security tab in SETTINGS. 

![image](https://github.com/Griche414/acit2420-assignment1/blob/main/Assets/Settings.png)

4.



## Installation



## Resources

   https://www.cloudflare.com/learning/access-management/what-is-ssh/

