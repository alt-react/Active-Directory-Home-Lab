# Active Directory Home Lab 

## Objectives

To document the entire process of setting up a home lab to be used to gain experience while doing hands-on cyber security portfolio projects.

1) Set up a Home Lab in VirtualBox consisting of 4 VirtualBox virtual machines:

     * 1 Windows 10 machine          
     * 1 Kali Linux Machine
     * 1 Windows Server 2022 machine
     * 1 Ubuntu Server machine       
    
    ![homeLabVMs](https://github.com/alt-react/Active-Directory-Home-Lab/assets/170683744/6be2c0df-a5c2-4eff-a646-3d03f733b11c)
                                            
3) Install and configure Sysmon and Splunk on our:

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
- Windows Media Creation Tool
- Sysmon
- Splunk SIEM

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

   * search for "windows server 2022 iso" and click the "Windows Server 2022 | Microsoft Evaluation Center" link
   * click "Download the ISO" link, then fill out the information, and click the blue "Download Now" button
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
   * after installation, enter secure password, then click "Finish"

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
   * at the "Guided storage configuration menu, use the down arrow to navigate to "Done" option, then hit "enter"
   * at the "Storage configuringation menu", use the down arrow to navigate do "Done", hit "enter", then go to "Continue" and hit enter
   * at the "Profile setup screen", enter whatever name, server name, username, and password you like, then navigate to "Done" and hit "enter"
   * hit "enter" to skip "Ubuntu Pro"
   * install "Open SSH" if you'd like
   * install whatever "Featured server snaps" you's like, then navigate to "Done" and hit enter
   * after installation, navigate to "reboot now" option, then hit "enter"
   * if you see "cdrom failed to unmount error". hit "enter"

</details>

___

### Configure virtual network

<details>
<summary>Set VirtualBox settings to NAT network</summary>
<br>
   
   Why? So that  virtual machines can be on the same network, and still have internet access
   

</details>










<!--
option 1

# PROJECTNAME

## Objective
[Brief Objective - Remove this afterwards]

The Detection Lab project aimed to establish a controlled environment for simulating and detecting cyber attacks. The primary focus was to ingest and analyze logs within a Security Information and Event Management (SIEM) system, generating test telemetry to mimic real-world attack scenarios. This hands-on experience was designed to deepen understanding of network security, attack patterns, and defensive strategies.

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
