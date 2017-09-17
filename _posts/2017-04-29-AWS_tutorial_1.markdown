---
layout: post
title:  "AWS Tutorial 1: What Is Cloud, Create and Connect to EC2"
date:   2017-04-29 10:35:00 -0700
categories: AWS
---

**Abstract:** What is cloud? Create an Ubuntu 16.04 virtual server. Connect to the server from a local machine. Stop and restart server. AWS pricing details.


**Reader:** Friends who plan to use cloud.


**Time:** 3000 words, 10min Reading, 10min Operating

**Prerequisite:** An AWS account



First, let's talk about what is cloud. Usually, when we use a personal computer, the keyboard is physically linked to the motherboard within the machine. And the machine is near us, most likely on the desk or under the desk. Some people may have used software called "Remote desktop" or similar services. At that time, we are using our keyboard on our desk to control someone else's PC. When we want to perform large scientific computation, people always use a tool called command line to remotely connect to another computer. In this case, we use a local keyboard to remotely control a powerful computer, a server we call. Normally, organizations like companies and schools have their own internal servers. They are collected and put together in a place called computer center or alike. Only the internal people in that organization have the access to those internal servers. When one company create a computer center and allows people around the world to access to and control the servers within it, we call that computer center as "Cloud".

A funny metaphor would be, imagine you entered into an Internet cafe, where there are only keyboards , mouse, and monitors. Then the manager talks to the "Cloud", "Please turn on a computer, and connect the keyboard, the mouse, and the monitor at that seat to it." You can then remotely operate on that computer. One of the advantages of cloud is "pay as you use". If all you need to do is to write a word document or send an Email, the manager would say, "Please turn on a machine with slower CPU, lower memory, smaller disk." (Actually, you are sharing ONE physical machine with other users. So there is the calling of "virtual server.") Then the fee you have to pay is lower. If you want to play video games, Cloud would give you a machine that fulfills the hardware needs for those games. And if you want to perform large amount of scientific computations, Could would give you a super computer or several of them. When you are done with using the computer, the manager would tell the Could to turn off that machine. So you can choose the machine as you need, and pay as you use. Amazon is one of the companies that provide Cloud service very early, and very well.

Next, let's talk about some words. *AWS* is the abbreviation of *Amazon Web Service*. In this tutorial series, the abbreviation and the followings would be used. *EC2*, the abbreviation of *Elastic Compute Cloud* (They are not using ECC which I think is because ECC is already taken in other fields). And one more word, *Instance*. EC2 is just a concept. When you turn on an EC2 server, that server is an EC2 instance. It's like "Apple (fruit)" is just a concept we used in our conversations. But "an apple on your hand" that you are going to eat is an instance of that concept.

Now, let's focus on our main story today. You need an AWS account to follow the tutorial. ([Page](https://aws.amazon.com/free/) to sign up) If you are a new user to them, you will have a 12-month trial of a micro server. If you are an old customer to them and have used out of the free quota, then following this tutorial series will incur costs. Please check the price list on AWS official page.

## Choose a region

First, login to AWS, on the upper-right corner of the page, after your account name, there is a drop-down box for you to choose a region. In the drop-down box, there are several computer centers of AWS around the globe. You can choose one that is near to you. This will determine the speed for you to connect and control the server. If you have some specific requirement, like want to use GPU, then you have to select one  with GPU support. Just like there are several canteens in a college. Most people just go to the nearest one to them. But if one canteen has your favorite food, you then want to go there. The prices are different for different regions. Just like house prices are different at different locations.

## Create an EC2 instance

Click "**Services**" on the upper-left corner, type "**EC2**" in the search box, press "Enter", it will lead you to the "**EC2 Dashboard**" page. The first section in the middle of the page is "Resources", and the second section is "Create Instance". Click the blue button "**Launch Instance**" under the "Create Instance" section.

Next, there will be a series of steps. It's like the process of installing a new software on Windows system. Asks you where you want to install, do you want to create a shortcut on desktop, etc. The steps to launch a new EC2 might seem a little intimidating if you want to understand all the details of them. But we can use the default values at most place. For the first time, let's make the most necessary modifications only and keep the rest as default. In the later tutorials, you will get a better intuition of what they really mean and how to change them.

*Step1*, Choose an Amazon Machine Image (AMI). This is like: when you buy a Windows computer, there will be a Windows system and commonly used software like Word, Excel, etc.; while for a Macintosh computer, there will be a Mac OS system as well as software like Safari, Reminders. That's what AMI is doing. It is in charge of the pre-installed operation system and the software inside it. Let's choose "**Ubuntu Server 16.04 LTS (HVM), SSD Volume Type**".  As of writing (20170429), it is the forth choice. It is an open source and commonly used Linux system.

*Step2*, Choose an Instance Type. This is where you control the configuration of your hardware, i.e., how powerful is your machine. Say, you only need it to send an Email, then choose a low one; but if you want to use it to perform scientific computing or run AI models, then choose a high one. Let's choose the second one "**t2.micro**" for now. Then click "Next: Configure Instance Details" on the lower-right corner. (More: There are many types you can choose. Like those targeted for high usage of CPU, GPU, or memory, or for general usage. You can check the categories and the prices at the [pricing page](https://aws.amazon.com/ec2/pricing/on-demand/). The nomenclature is "Style.Size", just like the style and size of clothes. For example, c4.2xlarge, means optimized for CPU computing, 4th generation, and the size is 2x large. Generally, for the same size, the newer the generation, the higher the performance and the lower the price. Like c4.large is better then c3.large and is also cheaper. If you need to perform massive amount of GPU computing, p2 category is preferred for now, see [here](http://www.bitfusion.io/2016/11/03/quick-comparison-of-tensorflow-gpu-performance-on-aws-p2-and-g2-instances/) for reasons. The pricing page mentioned above has a trick. You can check the price for different regions/locations. In general, the price is higher if the house price at that location is higher. Like the unit price in Tokyo, Seoul and Singapore is very high while "N. Virginia", "Ohio" and "Oregon" is lower. "t2.micro" is eligible for free tier. Since this is for tutorial, we just choose it. It will cost you less and save Amazon's resources as using powerful machines to learn basics is kind of a waste of both your and Amazon's resources.)

*Step3*, This is some detailed configuration. We keep everything as default. But the item "Subnet" will be covered in later tutorials when we talk about increasing the storage. Click "**Next: Add Storage**".

*Step4*, This is to set the size for storage (disk). By default, it will use SSD. The black box below tells you that you have 30GB free tier SSD quota (across your whole account). **Let's change the Size(GiB) from default 8 to 15**. Because for later tutorials, 8GB might be too small. Then click "Next: Add Tags".

*Step5*, Add Tags. Keep as default, Click "**Next: Configure Security Group**". (More: Tag is set as key-value pair. Basically, you can put anything there. Like the name of the server: cat, dog, firstMachine, ..; function: AI, webServer, bioinformatics, …; Software: TensorFlow, Anaconda, …; Admin: AdminName. In short, put whatever you want. I think the handy part of tag is that when you launched a lot of servers, like a company that uses AWS and has tens or hundreds of servers, it can help you manage them.)

*Step6*, Configure Security Group. Keep as default. Click "Review and Launch". (This step will be covered when we talk about jupyter server or website server in later tutorials.)

*Step7*, Review. Just check the settings in Step1-6. If no problem, then click "Launch" on the lower-right corner.

*Step8*, It will prompt you to "Select an existing key pair or create a new key pair". Choose "**Create a new key pair**" in the first drop-down box. Then type a name in the "**Key pair name**" box. I'm going to use "tutorial", you can use any as long as keep it consistent throughout the tutorial. Click "**Download Key Pair**". This key pair is going to be needed to connect to the instance, keep it in a safe place in your computer. Then, click "Launch Instance" on the lower-right corner. (More: My understanding for key pair is it is like two secret signal when two agents meet. One says the first sentence, the other says the second. If they match, you can then connect to the server. So, you don't want to lose your key pair or being stolen. You have only one chance to download it, which is when you just clicked "Download key pair". The file you download is half of the key pair, called private key file. The server within Amazon will keep the other half, the public key file. In later tutorials, we will cover how to bypass the key pair generated by Amazon and use our own key pair to connect. By then, you can throw the file you downloaded.)

## Connect to EC2 instance

In EC2 Management Console page, under the first section "Resources", the first link is "Running Instances". It will lead you to the page to manage EC2 instances. Or, you can enter the instances management page through clicking "Instances" inside the left navigation bar. You will see the instance you launched just now. Left click on that instance, the second half of the page will show you the detailed description of it. There is an item called "IPv4 Public IP" (The second on the right). We need that value to connect to the instance. The header of the instances' table includes "Name, Instance ID, Instance Type, …". One of them is "Status Checks". When status is shown as "2/2 checks passed", it's time for us to connect to and use the server. (In most case, we can connect after the *Public_IP* is shown. But for some instance types, like GPU, we need to wait for a while. Waiting for *Public_IP* is like waiting for a personal computer to turn on, while status checking is to see whether that computer is running well on all aspects.)

Before the connection, we need to do some preparation. Most of the time, when we communicate with a computer (things like open a browser, watch video, play games), we are using a program called "desktop". We click the mouse, and it will show us some fancy windows. We are not directly communicate with CPU or memory card, the program "desktop" does, which serves as a medium for us to control the computer. But it will cost much of the CPU and memory resources to generate those fancy windows. And that's something not good for a server focusing on computation. So when we control a server, we use a tool called *Terminal* rather than *Desktop*. We can run "Shell" command lines inside the terminal to control the server. Each command corresponds to an operation. For example, when we create a new folder named "folder_name" on "Desktop", we usually right click and choose "New Folder", then type in "folder_name". While in Linux command line, it is this command `mkdir folder_name`. `mkdir` is the abbreviation of "make directory", followed an argument, "folder_name", which is the name you want to set. So "Desktop" and "Terminal" are both media for us to communicate with computer, but the first one is more user-friendly, while "Terminal" is more cost-effective and actually faster when you get used to it. So, to connect to the server, we need a "Terminal" and a "Shell". 

For Windows users, I recommend [babun](http://babun.github.io/), it has *zsh* integrated in (babun is a terminal, zsh is a shell). For Mac users, I recommend [iTerm2](https://www.iterm2.com/), and then install [zsh](https://gist.github.com/kevin-smets/8568070). If you do not want to bother with it, you can just use the built-in terminal on Mac called "Terminal" (uses bash as shell). It is also very good. The commands later in the tutorial are supposed to be run in *zsh* or *bash*. 

Next, let's connect to the server. Open terminal (babun, or iTerm2 or Terminal), enter the directory containing "tutorial.pem" previously downloaded from AWS. Since I saved at "Downloads" directory, so I use command `cd Downloads` and then press enter. "cd" is the abbreviation of change directory. Then, run command `chmod 400 tutorial.pem` . This is to change the permission of the private key file. **Attention: this command and the followings can only be run at the directory containing the private key, otherwise, you need to specify the full path to the private key.** Explanation: This is like, there are many documents in the file room, and for each document, only some people have the right to access and change it while others cannot. This command is saying: change the permission of this file such that only the command executed by you can view the file "tutorial.pem"; others, like the potential virus program, cannot view this file. 

Then, we find the *Public_IP* mentioned above in the AWS EC2 management page. Type in the following command. Change the Public_IP to you actual IP value, which is a serials of numbers separated by three dots. Hit Enter (All commands need to be typed in and hit enter to be executed) to connect to the server.

```bash
ssh -i tutorial.pem ubuntu@Public_IP
```

This sentence is to tell "Shell", I want to use private key file "tutorial.pem" as secret signal, use tool "ssh", use username "ubuntu", connect to the server with IP as *Public_IP*. "ubuntu" is the default user name under Ubuntu system. Before we execute this command, we are on our local machine. After execution, we are then inside the Shell of the EC2 server. And if you run command later, you are controlling the server. If you are connect to the server for the first time, you local Shell will ask you:

```
The authenticity of host 'Public_IP (Public_IP)' can't be established.
RSA key fingerprint is 2e:a1:77:26:9e:xx:40:da:3f:b5:xx:3b:89:11:xx:39.
Are you sure you want to continue connecting (yes/no)?
```

An analogy for this question is that your local computer does not recognize the remote server (because they just met the first time), do you want to continue connecting. Enter "yes" to continue. Then you will see the following welcome message.

```bash
➜  Downloads ssh -i tutorial.pem ubuntu@34.210.62.130
Welcome to Ubuntu 16.04.2 LTS (GNU/Linux 4.4.0-1013-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.
```

We can use command `ls /` to view the root directory's contents:

```bash
ubuntu@ip-172-31-2-87:~$ ls /
bin   dev  home        lib    lost+found  mnt  proc  run   snap  sys  usr  vmlinuz
boot  etc  initrd.img  lib64  media       opt  root  sbin  srv   tmp  var
```

Then we can use

```bash
exit
```

to exit the server. The command to change the permission of the private key file only need to be executed once. So you can directly try the `ssh` command to connect the EC2 server again, and then exit.

## Stop, eboot, and terminate EC2 instance, EC2 pricing

Like a personal computer, you can buy it, turn it on, turn it off, reboot it, or even sell/throw away it; you can do all of these to a EC2 server. When we create a EC2 instance through the 7 steps mentioned above, we are kind of buying a machine, when you click "launch", it's like turn it on. In the EC2 management page, click "Instances" in the left navigator bar to check all the instances you created. Right click on the instance, Click "Instance State", you will see "Start, Stop, Reboot, Terminate". When you Stop it and then Start it, the Public_IP will change; but if you reboot it, Public_IP will not change. Terminate, is the action you want to perform when you do not need this server forever.

Some pricing details: Every time you start an EC2 instance, it will charge you one instance hour at the time you start it, and when it has been run for one hour, you will be charged another hour. So, if you start an EC2 instance, run for 1h59min, it will charge you 2h. However, if you start an EC2 instance, and stop, start it again within one hour, you will be charged two hours too. Because you start it twice. See [this page](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Stop_Start.html) for more. When you *Stop* it, AWS only charges you for EBS storage. The price for EBS is listed [here](https://aws.amazon.com/ebs/pricing/?nc1=h_ls). When you *Terminate* it, it will not charge you anymore, because it has deleted everything about that instance.



In the later tutorials, we will be using basic commands in Linux/Unix, like `ls`, `cd`, `cp`, `mv`, `top`, `sudo`, etc. You can find useful materials in section "further reading".



## Further reading

1. Getting Started with Amazon EC2 Linux Instances [official guide](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html)
2. [Connecting to Your Linux Instance Using SSH](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstancesLinux.html)
3. [UNIX Tutorial for Beginners](http://www.ee.surrey.ac.uk/Teaching/Unix/) 




## Take-home card

1. Login to AWS, choose a region, enter EC2, choose "Launch EC2, Ubuntu Server 16.04 LTS (HVM), SSD Volume Type， t2.micro", download private key.
2. `chmod 400 tutorial.pem` change the private key's permission.
3. `ssh -i tutorial.pem ubuntu@Public_IP` connect to the server.

