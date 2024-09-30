# 2420 assignment 1

This guide aims to guide you through the steps of creating a remote server using DigitalOcean and setting up an Arch Linux Droplet using ```cloud-init```.

Topics the guide will cover:
- Creating ssh keys and add them to your DigitalOcean account
- Adding a custom Arch Linux image
- Creating a droplet running Arch Linux
- Using cloud-init to:
    - Create a new regular user
    - Install some initial packages
    - Add a public SSH key to the authorized_keys file in your new user home directory
    - Disable root access via SSH


## Creating ssh keys and add them to your DigitalOcean account
The Secure Shell (SSH) protocol is a method you can use to securely transfer messages to a computer across an unsecured network. Furthermore, this method uses cryptography to verify identities and encrypts communication between your devices.

To create your ssh key:

1. Open your terminal
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

1. Log into your DigitalOcean account.

2. Click on settings on the left sidebar of your screen. 

![image](https://github.com/Griche414/acit2420-assignment1/blob/main/Assets/image1.png)

3. Click on Security tab in SETTINGS. 

![image](https://github.com/Griche414/acit2420-assignment1/blob/main/Assets/Settings.png)

4.Click on add SSH Key and paste your key that you copied with the command into the box below.

![image](https://github.com/Griche414/acit2420-assignment1/blob/main/Assets/SSHKeypng)

5. Name your key.

Once completed all the steps, it should look like this:

![image](https://github.com/Griche414/acit2420-assignment1/blob/main/Assets/NewSSH.png)

You have successfully added your SSH key to your DigitalOcean account


## Adding a custom Arch Linux image
We will create a server using DigitalOcean and for this manual, we will use ArchLinux as the Linux distrubution.
To do so:
1. Enter the following URL:https://gitlab.archlinux.org/archlinux/arch-boxes/-/packages/1545

2. Download the following Arch Linux  ```qcow2``` file.

![image](https://github.com/Griche414/acit2420-assignment1/blob/main/Assets/linuximg.png)
we will use qcow2 because it is easy to use and offers better performance.

You have sucessfully downloaded the Arch Linux image for creating a dropet.

## Creating a droplet running Arch Linux
To use the Arch Linux image we downloaded, we must first create a DigitalOcean droplet. To do so:
1.Click on Create and select Droplets

![image](https://github.com/Griche414/acit2420-assignment1/blob/main/Assets/createdroplet.png)

2. Click on San Francisco as the region.

![image](https://github.com/Griche414/acit2420-assignment1/blob/main/Assets/sanfran.png)

3. Select San Francisco Datacenter 3 - SFO3

![image](https://github.com/Griche414/acit2420-assignment1/blob/main/Assets/03.png)

4. Click Custom images from Choose an image section and select the Arch Linux file we downloaded.

![image](https://github.com/Griche414/acit2420-assignment1/blob/main/Assets/customimg.png)

5. Select Arch Linux as the distrubution.

7. Repeat steps 2 and 3, then click on Upload Image.

![image](https://github.com/Griche414/acit2420-assignment1/blob/main/Assets/uploadimg.png)

8. Go pack to previous page and Select the Arch Linux Image you uploaded. 

8. Click on Basic Plan.

9. Click on either Premium AMD or Premium Intel and select cheapest plan.

![image](https://github.com/Griche414/acit2420-assignment1/blob/main/Assets/plan.png)

10. Click on SSH Key from Choose Authentification Method. By default, the SSH Key you created is automatically selected.

![image](https://github.com/Griche414/acit2420-assignment1/blob/main/Assets/KeyFun.png)

11. Select 1 Droplet as we only need one droplet for this guide. It is the dafault option.

12. Type in a Host Name.

## Use a cloud-init configuration file to automate initial setup tasks

With your newly generated SSH key and the Arch Linux Image, we will now setup a cloud-init config file. Cloud-init enables you to skip most of the manual setup that is tedious, especially when you're creating multiple servers. 

To start the cloud-init config procedure: 
1. Use your Preferred text editor. For this manual, we will use notepad
2. Create a new txt.file and save it as ```cloud-config.yml```
3. Paste the following text into your text editor:
```#cloud-config
users:
  - name: <New Username>
    primary_group: <Group Name>
    groups: wheel
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    shell: /bin/bash
    ssh-authorized-keys:
      - ssh-ed25519 <Your Public Key> <Your Email>

packages:
  - ripgrep
  - rsync
  - neovim
  - fd
  - less
  - man-db
  - bash-completion
  - tmux

disable_root: true
```

4. Replace the ```name``` and ```primary_group``` with your windows username.
5. ```ssh-authorized keys``` will be replaced with the public key you used.

6. Going back to the droplet creation, click Advanced Options
7. Click on Add Initialization scripts (free).
8. Paste the block of text into the empty text box.
9. 
![image](https://github.com/Griche414/acit2420-assignment1/blob/main/Assets/yml.png)

10. Click on Create Droplet.

You have successfully created your first Droplet.



## Resources

   https://www.cloudflare.com/learning/access-management/what-is-ssh/
   https://gitlab.com/cit2420/2420-notes-f24/-/blob/main/2420-notes/week-two.md
   https://www.vinchin.com/vm-tips/raw-vs-qcow2.html
   https://www.digitalocean.com/community/tutorials/how-to-use-cloud-config-for-your-initial-server-setup

