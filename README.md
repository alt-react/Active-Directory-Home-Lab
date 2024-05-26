# Active Directory Home Lab 

## Objectives

> [!NOTE]
> To document the entire process of setting up a home lab to be used to gain experience while doing hands-on cyber security portfolio projects.
> 
> This repository will be updated in real-time as I progress through this project, so star it if you want to follow along.

___

1) Create 4 different virtual machines in VirtualBox:

     * 1 Windows 10 machine          
     * 1 Kali Linux Machine
     * 1 Windows Server 2022 machine
     * 1 Ubuntu Server machine       
    
    ![homeLabVMs](https://github.com/alt-react/Active-Directory-Home-Lab/assets/170683744/6be2c0df-a5c2-4eff-a646-3d03f733b11c)

2) Create a network in VirtualBox, and add our virtual machines to that same network

3) Configure static IP addresses on each virtual machine
                                            
4) Install and configure Sysmon and Splunk on our:

   * Windows 10 machine and
   * Windows Server 2022 machine

     so they can:

   * collect telemetry 
   * send log to a Splunk server

### Tools Used

<details>
<summary>- x86-64 Windows PC - for running the required software</summary>
<br>

   * minimum specs
      * 4-core processor
      * 16 GB RAM
      * 250 GB free storage
</details>

- Draw.io - for creating the network diagram
- VirtualBox - for creating the virtual network and the virtual machines
- Windows Media Creation Tool - to get Windows 10 ISO
- Sysmon - to collect telemetry
- Splunk SIEM - to organize and analyze logs

## Steps
<details>
<summary>Create the network diagram</summary>
<br>

  ![AltReact-Initial_Network_Diagram-50%](https://github.com/alt-react/Active-Directory-Home-Lab/assets/170683744/ce5c58f5-1c5c-4503-8424-2a74cc196a04)

  * you can do this in [Draw.io](https://www.draw.io)

</details>

___

### Create Virtual Machines

<details>
<summary>Download and install VirtualBox</summary>
<br>
   
   * go to https://www.virtualbox.org/wiki/Downloads to download VirtualBox for your system
   * verify SHA256 checksum to ensure the integrity of the download
   * install VirtualBox
</details>

<details>
<summary>Create the Windows 10 virtual machine in VirtualBox</summary>
<br>

  Download the Windows 10 ISO file

   * go to https://www.microsoft.com/en-ca/software-download/windows10 and click the blue "Download Tool now" button
   * run the installation file, choose the "Create installation media (USB flash drive, DVD, or ISO file) for another PC" option, and click next.
   * choose your desired language, architecture, and edition (or leave it as default), then click next
   * choose the ISO file option, then click next, then choose your download location

  Configure the virtual machine environment to use for Windows 10 installation
   
   * click the "New" button (blue spikey orb icon) in VirtualBox
   * enter the desired name of this virtual machine in the "Name" field
   * choose the desired location for your virtual machine in the "Folder" section
   * select the Windows 10 ISO file you downloaded in the "ISO Image" section
   * for a manual Windows install select the "Skip Unattended Installation" option, or leave deselected, then click "Next"
   * choose the desired RAM amount and number of CPUs to use for this virtual machine, then click "Next"
   * choose the desired storage configuration, then click "Next"
   * if you are happy with the configuration summary, click "Finish"
   
  Install Windows 10 in the newly created virtual machine environment
   
   * click "Start" (green arrow icon) in VirtualBox to start the virtual machine
   * click "Next" in the Windows installer, then click "Install Now"
   * click "I don't have a product key", then select "Windows 10 Pro" and click  "Next"
   * click "accept license terms", then click "Next"
   * select "Custom: Install Windows only (advanced), then click "Next"
   
</details>

<details>
<summary>Create the Kali Linux virtual machine in VirtualBox</summary>
<br>

  Download the Kali Linux ISO file

   * go to [Kali.org/get-kali](https://www.kali.org/get-kali) and click "Virtual Machines"
   * select your architecture, then click "VIrtualBox"
   * once your virtual machine image downloads, make sure 7-zip is installed, then double-click the extracted Kali Linux VirtualBox image
   
  Run Kali Linux in VirtualBox
   
   * click "Start" (green arrow icon) in VirtualBox to start the virtual machine
   * login using "kali" as the username and "kali" as the password

</details>

<details>
<summary>Create the Windows Server 2022 virtual machine in VirtualBox</summary>
<br>

  Download the Windows Server 2022 ISO file

   * search for "Windows Server 2022 iso" and click the "Windows Server 2022 | Microsoft Evaluation Center" link
   * click the "Download the ISO" link, then fill out the information, and click the blue "Download Now" button
   * click the "64-bit edition" link to download the ISO

  Configure the virtual machine environment to use for Windows Server 2022 installation
   
   * click the "New" button (blue spikey orb icon) in VirtualBox
   * enter the desired name of this virtual machine in the "Name" field
   * choose the desired location for your virtual machine in the "Folder" section
   * select the Windows Server 2022 ISO file you downloaded in the "ISO Image" section
   * for a manual Windows install select the "Skip Unattended Installation" option, or leave deselected, then click "Next"
   * choose the desired RAM amount and number of CPUs to use for this virtual machine, then click "Next"
   * choose the desired storage configuration, then click "Next"
   * if you are happy with the configuration summary, click "Finish"
   
  Install Windows Server 2022 in the newly created virtual machine environment
   
   * click "Start" (green arrow icon) in VirtualBox to start the virtual machine
   * when Windows boots up, click "Next", then click "Install Now"
   * select "Windows 2022 Standard Evaluation (Desktop Experience)", then click "Next"
   * accept the "terms and agreements", then click "Next"
   * select "Custom: Install Microsoft Server Operating System only (advanced)", then click "Next"
   * after installation, enter a secure password, then click "Finish"

</details>

<details>
<summary>Create the Ubuntu Server virtual machine in VirtualBox</summary>
<br>

   Download the Ubuntu Server ISO file

   * go to [ubuntu.com](https://www.ubuntu.com), go to the products tab, and click "Ubuntu Server"
   * click the green "Download Ubuntu Server" button
   * click the green "Download 24.04 LTS" button to start the download (version 24.04 LTS was the latest version when writing this)

  Configure the virtual machine environment to use for Ubuntu Server installation
   
   * click the "New" button (blue spikey orb icon) in VirtualBox
   * enter the desired name of this virtual machine in the "Name" field
   * choose the desired location for your virtual machine in the "Folder" section
   * select the Ubuntu Server IOS file you downloaded in the "ISO Image" section
   * for a manual Windows install select the "Skip Unattended Installation" option, or leave deselected, then click "Next"
   * choose the desired RAM amount and number of CPUs to use for this virtual machine, then click "Next"
   * choose the desired storage configuration, then click "Next"
   * if you are happy with the configuration summary, click "Finish"
   
  Install Ubuntu Server in the newly created virtual machine environment
   
   * click "Start" (green arrow icon) in VirtualBox to start the virtual machine
   * select "Try or Install Ubuntu Server" and hit the enter key
   * hit enter 6 times for default settings
   * at the "Mirror check still running" section, choose "continue", and hit enter
   * at the "Guided storage configuration" menu, use the down arrow to navigate to the "Done" option, then hit "Enter"
   * at the "Storage configuration menu", use the down arrow to navigate to "Done", hit "enter", then go to "Continue" and hit enter
   * at the "Profile setup screen", enter whatever name, server name, username, and password you like, then navigate to "Done" and hit "enter"
   * hit "enter" to skip "Ubuntu Pro"
   * install "Open SSH" if you'd like
   * install whatever "Featured server snaps" you'd like, then navigate to "Done" and hit enter
   * after installation, navigate to the "reboot now" option, then hit "enter"
   * if you see "cdrom failed to unmount error". hit "enter"

</details>

___

### Set up and configure the Home Lab network in VirtualBox

<details>
<summary>Create a NAT network in VirtualBox</summary>
<br>

   1) open VirtualBox, click on "Tools", then click on "Network"
   2) click the "NAT Networks" tab, then click the "Create" button
   3) click on the newly created "NatNetwork" then change "Name" to whatever you like (optional)
   4) change the "IPv4 Prefix" to the prefix you defined in the network diagram you created
   5) leave "Enable DHCP" checked, and hit "Apply"

</details>

<details>
<summary>Add our virtual machines to the NAT network we  created in VirtualBox</summary>
<br>

For each of the 4 virtual machines, complete the following steps:

   1) click on the virtual machine, click "Settings", then click "Network"
   2) in the "Adapter 1" tab, click inside the "Attached to:" dropdown menu and choose "NAT Network"
   3) in the "Name" dropdown menu, make sure to select the NAT network that you created in step 3 in "Set up a virtual network in VirtualBox", then click "OK"

</details>

___

<details>
<summary>Configure static IP address on Ubuntu Server (Splunk SIEM) virtual machine</summary>
<br>

   1) start the Ubuntu Server (Splunk SIEM) virtual machine
   2) log in, type `ip a`, then hit "Enter" to see the virtual machine's current IP address
   3) type in `sudo nano /etc/netplan/00-installer-config.yaml`, then hit the "enter" key
   4) enter:

            network:
                ethernet:
                    enpos3:
                        dhcp4: no
                        addresses: [192.168.10.10/24]
                        nameservers:
                            addresses: [8.8.8.8]
                        routes:
                            - to: default
                              via: 192.168.10.1
                version: 2
   5) hit the "ctrl + x" keys, press y, then hit "Enter" to save the file
   6) type `sudo netplan apply` and hit "Enter"
   7) type `ip a` again, to verify that our IP address is 192.168.10.10
   8) type in `ping google.com` and hit "Enter" to verify the internet connection through our server
   9) hit the "ctrl + c" keys to stop the ping command

</details>

___

<details>
<summary>Download and install Splunk on Ubuntu Server (Splunk SIEM)</summary>
<br>

   1) on your host machine (not on any of your virtual machines, but on the machine running your virtual machines), go to [splunk.com](https://www.splunk.com), sign up with an account, and log in
   2) got to the "Products" tab, then click on "Free Trials & Downloads"
   3) scroll down to "Splunk Enterprise" and click on "Get My Free Trial"
   4) under "Choose Your Installation Package", click the "Linux" option, then click the "Download Now" button for the ".deb" option
   5) scroll through the Splunk General Terms document, click the "I have read, understood, etc" box, then click the Access program" button to start the Splunk download
   6) on your Ubuntu Server virtual machine, type `sudo apt install virtualbox-guest-additions-iso` and hit "Enter"
   7) type in `y`, then hit "Enter" to start the virtualbox-guest-additions-iso installation
   8) in the virtual machine window, click the "Devices" tab, hover over "Shared Folders", and select "Shared Folder Settings"
   9) click on the blue folder icon towards the top-right of the window to add a folder
   10) in the "Folder Path:" section, choose "Other", and add the path to the "splunk*.deb" file we downloaded earlier
   11) leave the "Folder Name:" section as is, then select the "Read-only", "Auto-mount", "Make-Permanent" options, click "OK", then click "OK" again
   12) in our Ubuntu Server command line interface, type `sudo reboot` and hit "Enter"
   13) log back into the Ubuntu Server, type in `sudo apt install virtualbox-guest-utils`, then hit "Enter"
   14) type `sudo adduser *your username* vboxsf` and hit "Enter", type `sudo reboot` and hit "Enter"
   15) log back into the Ubuntu Server, then type `sudo adduser *your username* vboxsf`, and hit "Enter"
   16) type 'mkdir share', hit "Enter", then type `ls`, and hit "Enter"
    
    
    
</details>





<!--
option 1

# PROJECTNAME

## Objective
[Brief Objective - Remove this afterwards]

The Detection Lab project aimed to establish a controlled environment for simulating and detecting cyber attacks. The primary focus was to ingest and analyze logs within a Security Information and Event Management (SIEM) system, generating test telemetry to mimic real-world attack scenarios. This hands-on experience was designed to deepen my understanding of network security, attack patterns, and defensive strategies.

### Skills Learned
[Bullet Points - Remove this afterwards]

- Advanced understanding of SIEM concepts and practical application.
- Proficiency in analyzing and interpreting network logs.
- Ability to generate and recognize attack signatures and patterns.
- Enhanced knowledge of network protocols and security vulnerabilities.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used
[Bullet Points - Remove this afterwards]

- Security Information and Event Management (SIEM) system for log ingestion and analysis.
- Network analysis tools (such as Wireshark) for capturing and examining network traffic.
- Telemetry generation tools to create realistic network traffic and attack scenarios.

## Steps
drag & drop screenshots here or use imgur and reference them using imgsrc

Every screenshot should have some text explaining what the screenshot is about.

Example below.

*Ref 1: Network Diagram*

option 2

<h1>JWipe - Disk Sanitization</h1>

 ### [YouTube Demonstration](https://youtu.be/7eJexJVCqJo)

<h2>Description</h2>
Project consists of a simple PowerShell script that walks the user through "zeroing out" (wiping) any drives that are connected to the system. The utility allows you to select the target disk and choose the number of passes that are performed. The PowerShell script will configure a diskpart script file based on the user's selections and then launch Diskpart to perform the disk sanitization.
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Diskpart</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)

<h2>Program walk-through:</h2>

<p align="center">
Launch the utility: <br/>
<img src="https://i.imgur.com/62TgaWL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Select the disk:  <br/>
<img src="https://i.imgur.com/tcTyMUE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Enter the number of passes: <br/>
<img src="https://i.imgur.com/nCIbXbg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Confirm your selection:  <br/>
<img src="https://i.imgur.com/cdFHBiU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/K71yaM2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

dropdown menu in markup
<details open>
<summary>Want to ruin the surprise?</summary>
<br>
Well, you asked for it!
</details>

 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
