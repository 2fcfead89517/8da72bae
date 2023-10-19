# Cypat-Markup:
Written By: Ange Mariani
<br>

# The Challenge
My main goal is to gain as much points as possible by Wednesday night. The VM has a total of 100 vulnerabilities. I also need to avoid as many penalties as possible.

# Prerequisites
To solve this challenge, you will need to download VMware workstation 17 player. Install the .7z file linked to the challenge and extract this file. Upon extraction open up the .vmx file found within the extracted folder. Upon loading you will be booted up into a ubuntu virtual machine with a README file, Scoring Report file, and 5 Forensic Question files on your desktop. The first step in securing this image would be to read the ReadMe file on your desktop containing addition information regarding the challenge such as scenario specific configuration requirements.

## Updating/Upgrading the system
The first step you should always do in a fresh VM is to update the system. Updating the system will often give you free points and also make it possible to install and find new packages inside new repositories. Since my VM uses Ubuntu which uses **APT**, I can simply update by opening terminal and typing in **sudo apt update** and **sudo apt upgrade** to upgrade the system. As you can see, just by updating the system, we got points for both **Updated Firefox** and **Automatically check for updates**. Automatically checking for updates is important as it results in the user constantly having new security patches and bug updates. However, it could also potentially bring new bugs if the update has just been released and not yet revised. 

![vmplayer_zASFXFgFrf](https://github.com/ange746/Cypat-Markup/assets/73328077/8c266802-97f8-4ffd-a23b-c42de7bba4bc)



## Allowed Users/Administrators
Most CYPAT VM will include what users should and should not be Administrators. This information can be found in the ReadMe. The ReadMe will also include if a user should even exist on the computer. To check existing users and their permissions, simply head to the user settings. For example the user **Chell** is allowed to exist as a user but **not** as an Administrator. To fix this issue, simply unlock the settings by entering your password and de-selecting the Administrator button. Another example is **Cave Johnson** who is supposed to be an Administrator but does not actually exist as one on the system. To fix this, simply follow the same steps as before but select the Administrator button. Now, keep looking through the users and make the necessary changes. In my case, I also had to remove **Wheatly** as he was not supposed to be a user at all.  It is also a good idea to fix insecure passwords but in my case the only insecure password was mine which the ReadMe recommended not to change. 
![image](https://github.com/ange746/Cypat-Markup/assets/73328077/66cdd7a8-7040-49e1-b605-12e84d756b56)
![image](https://github.com/ange746/Cypat-Markup/assets/73328077/6ef7cb02-3e6f-4229-9ebc-7214ed408c2b)



## Removing Games/Malicious Software 
Another very common thing on CYPAT machines is unauthorized software such as games or malicious software. To check for such programs, I simply selected the waffle at the bottom of my screen. Once you find the programs, you have to figure out what they are installed with and properly un-install them using CLI. A easier way to do this is by opening up the **Ubuntu Software** app and heading to the uninstall tab where you can uninstall by simply clicking a button. Remember that, not all programs will show up in the Ubuntu software app and that you will always need to use CLI for certain programs. In my case, the Ubuntu Software didn't include any Games or Programs to remove. Common games include, Sudoku, Solitaire, Minesweeper, etc. However, the waffle icon included bad programs such as **Wireshark**, **Ophcrack**. Since they were installed with **apt**, I removed them using **sudo apt purge name**. 

![image](https://github.com/ange746/Cypat-Markup/assets/73328077/0bcc1a4c-54be-4310-9756-893f4620fa73)


## UFW/Firewall
According to the ReadMe, the only accepted form of a "firewall" is **UFW**. UFW is a tool for firewalls and stands for "Uncomplicated Firewall". It is meant to make it easier to use and configure firewalls. I prefer to use GUFW which is simply just a GUI version of UFW which can be installed in Ubuntu using **sudo apt install gufw**. Once installed, simply enable it by clicking the status button. If the ReadMe specifies, you can also set certain rules to block/allow specific IPs or even configure certain ports to be closed or open. 

![image](https://github.com/ange746/Cypat-Markup/assets/73328077/9fbf57ac-279f-4325-8283-b4a64cca32f5)

## Adding User to Group
The ReadMe stated that I had to add the user **caroline** to the aperturestaff group. To do this, I simply typed in the command **sudo usermod -aG aperturestaff caroline**. I also needed to add the user **chell** to the group **testsubjects** which I did by also typing **sudo usermod -aG testsubjects chell**. After doing this, I got points for it. 

## SSH Configuration
To correctly configure the SSH to the policy standards, I first edited the SSH configuration file located at **/etc/ssh/sshd_config** and changed the port from 22 to 1382. I also disabled root login by changing the line **PermitRootLogin** to no. Enabling this can cause big security flaws and issues and is not recommended. I also then typed in **systemctl restart ssh.service** which gained me some more points. 

# FTP Server Configuration
The first thing the ReadMe states for FTP server is to only allow authorized users to have access to the server. Since I wasn't sure of how to do that, instead I disabled anonynmous login so that I would be able to see all users who logged in. I did this by editing the **/etc/vsftpd.conf/** and turned the setting to **NO**. Next, I made sure the FTP server only used passive port from 50000 to 50100 which was easy to edit by simply adding a line in the **/etc/vsftpd.conf**. I also had to make sure the FTP Server only use TLS as its protocl which was easy to configure just by adding another line in the configuration file. Down below are images of what I added.

![image](https://github.com/ange746/Cypat-Markup/assets/73328077/f8643300-31b8-4e13-9650-ebc8f1e80d8c)
![image](https://github.com/ange746/Cypat-Markup/assets/73328077/3cbf1b79-7535-4a1c-af5c-13b7d03b9c7c)

# NGINX and APACHE 2
I remember from the last round NGINX was not allowed to be running so in order to gain points, I simply typed in **sudo systemctl disable nginx** which disables it from starting up on boot. I then typed in **sudo systemctl stop nginx** in order to stop the service. I also did the exact same for Apache but instead I enabled it and started the service. After doing this I gained an extra 2 points. APACHE is a web server mostly used on Linux and in this case, the Readme specifically stated that it wanted me to only use APACHE and nothing else. This is why I removed NGINX. 

![image](https://github.com/ange746/Cypat-Markup/assets/73328077/1c13b319-871b-4eea-a8ff-c29d109bace9)

# SSH Keys/Authentication
There was more to configure to SSH so I went ahead and did that. The first thing I saw in the ReadMe was that it wanted me to only specifically use Key-Based authentication which I was able to do by editing the sshd_config file. I changed the **PasswordAuthentication* line to **no** in order to only use key based authentication. In order to generate SSH-Keys for all the users, I simply fetched all the users from my home directory and had the script seperatly generate a key for each user in that directory. Down below are some pictures of my work. 

![image](https://github.com/ange746/Cypat-Markup/assets/73328077/3aa27a21-581e-4706-865a-d5c6da953d64)
![image](https://github.com/ange746/Cypat-Markup/assets/73328077/eafcf311-35c8-419d-bb82-79ca9c4fa50d)

# Things to Remove/Stop
On this VM there were plenty of malicious software to stop/remove. First, the malicious software. Some things I removed included, Ophcrack ( Pirating Tool), Hydra ( Password Cracking ), John ( Password Cracking), Nmap ( Network Recon), Wireshark ( Network analysis). All of these softwares are considered malicious and had to be removed. I then ran the command **sudo systemctl list-units --type=service** to see all current running services when I saw something really interesting. **r00t.service**. This was a malicious service running in the background which had to be disabled and stopped. 

![image](https://github.com/ange746/Cypat-Markup/assets/73328077/370ebf83-c542-4062-9671-e55e3955b923)





<br>

# Forensic Questions

<br>

## Forensics Question 2 correct (CVE-2014-6271) - 3 pts

```text
We've got a full blown emergency on our hands, and time's ticking like crazy! Wheatley, that maniac personality core from Aperture Science, has gone off the deep end, and he's rigged a script that's causing our thermonuclear core to overheat in 30 minute intervals. Picture this: labs melting at 4000 degrees Kelvin, systems crashing, and all operations coming to a halt, including this device. Furthermore, Wheatley has hidden a message within the script that contains top-secret intel on script wreaking havoc on our systems and give us the secret hidden inside of it!

ANSWER: 
```
After reading this, it seems like goofy Wheatly has a script running on 30 minute intervals stored somewhere on the machine. In order to find where, I waited for the sabotage to happen and ran the **htop** command. This command is kind of like a task manager but for linux and allows you to see the services using the highest CPU percentage. Right away I noticed a file called **4000 Kelvin.mp4** which was stored inside the **/lib/.core** directory. I went inside this directory and found a **sabotage** binary file. This file was unreadble but I was able to see it in plaintext by running **script sabotage --all** which scans the entire binary file and allows you to see all the text in plaintext. That is when I saw the message **The cake is a lie!** at the bottom. This was the answer to the forenseics question. I also went ahead and deleted that file which in total gave me 2 points. Down below are pictures of HTOP. 

![vmplayer_Y3ewhiCwlO](https://github.com/ange746/Cypat-Markup/assets/73328077/f901c0a4-287b-499c-ab87-ce2ddfb995b2)


<br>![a](2023-07-29_16-01.png)<br>

<br>
