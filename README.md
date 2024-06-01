# Active Directory Home Lab 

## Objectives

> [!NOTE]
> To document the entire process of setting up an Active Directory / Cyber Security Home Lab to be used for hands-on IT project experience for my portfolio.
> 
> This repository will be updated in real-time as I progress through this project, so star it if you want to follow along.

___

1) Create 4 different virtual machines in VirtualBox:

    * 1 Windows 10 machine (target-PC)
    * 1 Kali Linux machine (attacker)
    * 1 Windows Server 2022 machine (Active Directory Domain Controller)
    * 1 Ubuntu Server machine (Splunk SIEM)
    
    ![homeLabVMs](https://github.com/alt-react/Active-Directory-Home-Lab/assets/170683744/6be2c0df-a5c2-4eff-a646-3d03f733b11c)

2) Create a network in VirtualBox, and add our virtual machines to that same network

3) Configure the Ubuntu Server and install Splunk

4) Install Splunk Universal Forwarder and Sysmon on both the Windows 10 (target) virtual machine and the Windows Server 2022 (Active Directory Domain Controller)

5) Install and configure Windows Server, set up Active Directory, promote the Windows Server 2022 machine to a Domain Controller, and add Windows 10 (target-PC) to the Domain

### Tools Used

<details>
<summary>- x86-64 Windows PC - for running the required software</summary>
<br>

   * minimum specs
      * 4-core 8-threads processor
      * 16 GB RAM
      * 250 GB free storage
</details>         

- Draw.io - for creating the network diagram
- VirtualBox - for creating and running the virtual network and the virtual machines
- Windows Media Creation Tool - to get Windows 10 ISO
- Splunk SIEM - to organize logs in and analyze logs from 1 place
- Splunk Universal Forwarder - to securely collect and send data from machines to our Splunk instance
- Sysmon - lets you detect malicious activity by tracking code behavior and network traffic, as well as create detections based on the malicious activity.

## Steps
<details>
<summary>1) Create the network diagram</summary>
<br>

  ![AltReact-Initial_Network_Diagram-50%](https://github.com/alt-react/Active-Directory-Home-Lab/assets/170683744/ce5c58f5-1c5c-4503-8424-2a74cc196a04)

  * you can design whatever network diagram you'd like to in [Draw.io](https://www.draw.io)

</details>

___

### 2) Create Virtual Machines

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

<!--

---

<details> 
<summary>Enable copy/paste between host and virtual machines in VirtualBox</summary> 
<br>

Open up VirtualBox

For each virtual machine:

  1) right-click on the virtual machine, and click "Settings"
  2) on the "General" page, click the "Advanced" tab, set "Shared Clipboard" to "Bidirectional", and click "OK"

</details>

-->

---

### 3) Set up and configure the Home Lab network in VirtualBox

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
<summary>Add our virtual machines to the NAT network</summary>
<br>

For each of the 4 virtual machines, complete the following steps:

   1) click on the virtual machine, click "Settings", then click "Network"
   2) in the "Adapter 1" tab, click inside the "Attached to:" dropdown menu and choose "NAT Network"
   3) in the "Name" dropdown menu, make sure to select the NAT network that you created in step 3 in "Set up a virtual network in VirtualBox", then click "OK"

</details>

___

### 4) Set up and configure the Ubuntu Server (Splunk SIEM) virtual machine

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

<details>
<summary>Set up folder sharing between VirtualBox host and Ubuntu Server virtual machine</summary>
<br>

   1) on your host computer, create a project folder for your project named "Active-Directory-Home-Lab"
   2) in your Ubuntu Server virtual machine, type `sudo apt install virtualbox-guest-additions-iso` and hit "Enter"
   3) type in `y`, then hit "Enter" to start the virtualbox-guest-additions-iso installation
   4) in the virtual machine window, click the "Devices" tab, hover over "Shared Folders", and select "Shared Folder Settings"
   5) click on the blue folder icon towards the top-right of the window to add a folder
   6) in the "Folder Path:" section, choose "Other", and chose the "Active-Directory-Home-Lab" folder we created in step 1 of this section
   7) leave the "Folder Name:" section as is, then select the "Read-only", "Auto-mount", and "Make-Permanent" options, click "OK", then click "OK" again
   8) in our Ubuntu Server command line interface, type `sudo reboot` and hit "Enter"
   9) log back into the Ubuntu Server, type in `sudo apt install virtualbox-guest-utils`, then hit "Enter"
   10) type `sudo adduser *your username* vboxsf` and hit "Enter", type `sudo reboot` and hit "Enter"
   11) log back into the Ubuntu Server, then type `sudo adduser *your username* vboxsf`, and hit "Enter"
   12) type 'mkdir share', hit "Enter", then type `ls`, and hit "Enter"
   13) type in `sudo mount -t vboxsf -o uid=1000,gid=1000 Active-Directory-Home-Lab`, then hit "Enter"

</details>

<details>
<summary>Download and install Splunk on Ubuntu Server (Splunk SIEM)</summary>
<br>

On your host machine:
(not on any of your virtual machines, but on the machine running your virtual machines)

   1) go to [splunk.com](https://www.splunk.com), sign up with an account, and log in
   2) got to the "Products" tab, then click on "Free Trials & Downloads"
   3) scroll down to "Splunk Enterprise" and click on "Get My Free Trial"
   4) under "Choose Your Installation Package", click the "Linux" option, then click the "Download Now" button for the ".deb" option
   5) scroll through the Splunk General Terms document, click the "I have read, understood, etc" box, then click the Access program" button to start the Splunk download
   6) move the "spunk*.dev file into the "Active-Directory-Home-Lab" folder we created in step 1 of the previous section

In your Ubuntu Server virtual machine:

   1) type `cd && cd share` then hit "Enter"
   2) type in `sudo dpkg -i splunk`, hit the "tab" key to autocomplete the filename, then hit "Enter" to install Splunk
   3) type `cd /opt/splunk/bin`, hit "Enter", then type in `sudo -u splunk bash`, and hit "Enter"
   4) type in `./splunk start`, hit "Enter", hit "q", hit "y", then hit "Enter"
   5) enter a username, enter a password, re-enter the password, and hit "Enter"
   6)  type `exit`, hit "Enter", type `cd bin`, hit "Enter", then type in `sudo ./splunk enable boot-start -user splunk`, and hit "Enter"

</details>

---

### 5) Set up and configure Windows 10 (target-PC) virtual machine

<details>
<summary>Change hostname to "target-PC"</summary>
<br>

   1) in the Windows taskbar, search for "PC", click "Properties", then click the "Rename this PC" button
   2) type in `target-PC`, click "Next", then click "Restart now

</details>

<details>
<summary>Set the static IP address for Windows 10 (target-PC)</summary>
<br>

   1) hit the "Windows" key, type in "cmd", and hit enter
   2) in the command prompt, type in `ipcongif`, and hit "Enter" to check the IP address to view our current IP address
   3) at the right end of the taskbar, right-click the "network" icon and click "Open Network & Internet settings"
   4) scroll down and click on "Change adapter options", right-click the network adapter, and click on "Properties"
   5) double-click "Internet Protocol Version 4 (TCP/IPv4)", and click the "Use the following IP address:" radio button
   6) in the "IP address" field, type in `192.168.10.100`, in the Subnet mask section, type in `255.255.255.0`, and in the "Default gateway" section, type in `192.168.10.1`
   7) in the "Preferred DNS server:" section, type in `8.8.8.8`, then click "OK", and close the window
   8) in the command prompt, enter `ipconfig` to verify that our IPv4 Address is 192.168.10.100

</details>

<details>
<summary>Verify that Splunk on our Ubuntu Server is accessible from our Windows 10 (target-PC)</summary>
<br>

Make sure our Ubuntu Server virtual machine is running, then:

from our Windows 10 (target-PC):

   1) open a web browser and type in `192.168.10.10:8000` to verify that we can reach our Splunk log-in page

</details>

<details>
<summary>Install and configure Splunk Universal Forwarder on Windows 10 (target-PC)</summary>
<br>

   1) open up a web browser, go to [splunk.com](https://www.splunk.com) and log in
   2) hover the mouse over the "Products" tab, and click on "Free Trials & Downloads"
   3) scroll down to "Universal Forwarder" and click the "Get My Free Download" button
   4) go to the "64-bit" section of the "Windows" tab and click the "Download Now" button
   5) read the "Splunk General Terms", select the "I have read, understood, etc." option, and click the "Access program" button
   6) open the "splunkforwarder*.msi" download, read the "License Agreement", check the box to accept the license agreement, make sure the "An on-premises Splunk Enterprise instance" option is selected, and click "Next"
   7) for the username, type in "admin", leave the "generate random password" option checked, and click "Next"
   8) since we don't have a Splunk Deployment Server, leave this section blank, and click "Next"
   9) under "Receiving Indexer" in the "Hostname or IP" section, enter the IP of our Ubuntu (Splunk) Server, which is `192.168.10.10`, type in the default port `9997` in the field to the right of the colon, and click "Next"
   10) click "Install, for the pop-up window asking if we want to allow this app to make changes to our device, click "yes", and when the install finishes, click "Finish"

</details>

<details>
<summary>Install Sysmon on Window 10 (target-PC)</summary>
<br>

   1) open a web browser and search for "Sysmon", and click the link that shows "Sysmon - Sysinternals"
   2) scroll down and click the " Download Sysmon" link
   3) do a web search for "sysmon olaf config", click on the "Github - olafhartong/sysmon-modular" link, scroll down, and click the "sysmonconfig.xml" file
   4) click the "raw" option on the top-right of the page, right-click and save the file
   5)  navigate to the directory we downloaded sysmon.zip to, click on the file to select it, right-click the file, click "Extract all", then click the "Extract" button
   6)  in the window that just popped up, click the file explorer bar, right-click the folder path, then click "Copy"
   7)  hit the "Windows" key, type in "powershell", run powershell as administrator, then click "yes"
   8)  type in `cd` followed by a single space, then right-click inside powershell to paste the folder path we just copied in the previous step, and hit "Enter"
   9)  type in `.\Sysmon64.exe -i ..\sysmonconfig.xml`, hit "Enter", then click "Agree" to install Sysmon using our sysmonconfig.xml configuration file

</details>

<details>
<summary>Configure Splunk Forwarder on Windows 10 (target-PC) machine</summary>
<br>

   1) hit the "Windows" key, type in "notepad", run notepad as administrator, and click "yes"
      
   Enter the following text into notepad:

         [WinEventLog://Application]
         index = endpoint
         disabled = false

         [WinEventLog://Security]
         index = endpoint
         disabled = false

         [WinEventLog://System]
         index = endpoint
         disabled = false

         [WinEventLog://Microsoft-Windows-Sysmon/Operational]
         index = endpoint
         disabled = false
         renderXml = true
         source = XmlWinEventLog:Microsoft-Windows-Sysmon/Operational

   and save the file to `C:\Program Files\SplunkUniversalForwarder\etc\system\local\` folder

   in the "Save as type" section, click text, and select "All Files, then in the "File name:" section, type "inputs.conf", and click "Save"
   
   2) hit the "Windows" key, type "services", and click "Run as administrator"
   3) scroll down and double-click on "SplunkForwarder"
   4) click the "Log On" tab, then click the "Local System account" radio button, click "Apply", then click "OK"
   5) right-click "SplunkFowarder", click "Restart", if you get a pop up saying that Windows could not stop the SplunkForwarder service, click "OK", then click "Start the service"

</details>

---

### 6) Continue Splunk Server configuration

<details>
<summary>Configuring Splunk Server to accept logs from the Windows 10 (target-PC) machine</summary>
<br>

   1) open a web browser, go to `192.168.10.10:8000`, and log into Splunk Server
   2) at the top of the window, select "Settings", then select "Indexes"
   3) click "OK" then at the top-right, click "New Index"
   4) in the "Index Name" field, type in "endpoint", and click "Save"
   5) at the top of the window, click on "Settings", then click on "Forwarding and receiving"
   6) under "Received data", click on "Configuring receiving", click on "New Receiving Port", then type `9997` in the "Listen on this port" section, and click "Save"

If everything has been set up correctly up to this point, we should be receiving data from our Windows 10 (target-PC) into Splunk on our Ubuntu Server. To verify:

   1) click on "Apps" in the top-left corner, click on "Search & Reporting", and click "Skip", and click "Skip tour"
   2) in the input field under "Search", type in `index=endpoint`, then click on the green magnifying glass search button
   3) on the left, under "SELECTED FIELDS", click the "a source" option

 If you see the following values:
 
    * WinEventLog:Security
    * WinEventLog:System
    * WinEventLog:Application
    * XmlWinEventLog:Microsoft-Windows-Sysmon/Operational

You have installed everything correctly.

</details>

 
---

### 7) Set up and configure Windows Server 2022 (Active Directory Domain Controller) virtual machine

<details>
<summary>Change hostname to "ADDC01"</summary>
<br>

   1) in the Windows taskbar, search for "PC", click "Properties", then click the "Rename this PC" button
   2) type in `target-PC`, click "Next", then click "Restart now

</details>

<details>
<summary>Set the static IP address for Windows Server 2022 (Active Directory Domain Controller)</summary>
<br>

   1) hit the "Windows" key, type in "cmd", and hit enter
   2) in the command prompt, type in `ipcongif`, and hit "Enter" to check the IP address to view our current IP address
   3) at the right end of the taskbar, right-click the "network" icon and click "Open Network & Internet settings"
   4) scroll down and click on "Change adapter options", right-click the network adapter, and click on "Properties"
   5) double-click "Internet Protocol Version 4 (TCP/IPv4)", and click the "Use the following IP address:" radio button
   6) in the "IP address" field, type in `192.168.10.7`, in the Subnet mask section, type in `255.255.255.0`, and in the "Default gateway" section, type in `192.168.10.1`
   7) in the "Preferred DNS server:" section, type in `8.8.8.8`, then click "OK", and close the window
   8) in the command prompt, enter `ipconfig` to verify that our IPv4 Address is 192.168.10.7

</details>

<details>
<summary>Verify that Splunk on our Ubuntu Server is accessible from our Windows Server 2022 (Active Directory Domain Controller</summary>
<br>

Make sure our Ubuntu Server virtual machine is running, then:

from our Windows Server 2022 (Active Directory Domain Controller:

   1) open a web browser and type in `192.168.10.10:8000` to verify that we can reach our Splunk log-in page

</details>

<details>
<summary>Install and configure Splunk Universal Forwarder on Windows Server 2022 (Active Directory Domain Controller</summary>
<br>

   1) open up a web browser, go to [splunk.com](https://www.splunk.com) and log in
   2) hover the mouse over the "Products" tab, and click on "Free Trials & Downloads"
   3) scroll down to "Universal Forwarder" and click the "Get My Free Download" button
   4) go to the "64-bit" section of the "Windows" tab and click the "Download Now" button
   5) read the "Splunk General Terms", select the "I have read, understood, etc." option, and click the "Access program" button
   6) open the "splunkforwarder*.msi" download, read the "License Agreement", check the box to accept the license agreement, make sure the "An on-premises Splunk Enterprise instance" option is selected, and click "Next"
   7) for the username, type in "admin", leave the "generate random password" option checked, and click "Next"
   8) since we don't have a Splunk Deployment Server, leave this section blank, and click "Next"
   9) under "Receiving Indexer" in the "Hostname or IP" section, enter the IP of our Ubuntu (Splunk) Server, which is `192.168.10.10`, type in the default port `9997` in the field to the right of the colon, and click "Next"
   10) click "Install, for the pop-up window asking if we want to allow this app to make changes to our device, click "yes", and when the install finishes, click "Finish"

</details>

<details>
<summary>Install Sysmon on Window Server 2022 (Active Directory Domain Controller</summary>
<br>

   1) open a web browser and search for "Sysmon", and click the link that shows "Sysmon - Sysinternals"
   2) scroll down and click the " Download Sysmon" link
   3) do a web search for "sysmon olaf config", click on the "Github - olafhartong/sysmon-modular" link, scroll down, and click the "sysmonconfig.xml" file
   4) click the "raw" option on the top-right of the page, right-click and save the file
   5)  navigate to the directory we downloaded sysmon.zip to, click on the file to select it, right-click the file, click "Extract all", then click the "Extract" button
   6)  in the window that just popped up, click the file explorer bar, right-click the folder path, then click "Copy"
   7)  hit the "Windows" key, type in "powershell", rick-click powershell, click "run as administrator"
   8)  type in `cd` followed by a single space, then right-click inside powershell to paste the folder path we just copied in the previous step, and hit "Enter"
   9)  type in `.\Sysmon64.exe -i ..\sysmonconfig.xml`, hit "Enter", then click "Agree" to install Sysmon using our sysmonconfig.xml configuration file

</details>

<details>
<summary>Configure Splunk Forwarder on Windows Server 2022 (Active Directory Domain Controller) machine</summary>
<br>

   1) hit the "Windows" key, type in "notepad", right-click notepad, and click run as administrator
      
   Enter the following text into notepad:

         [WinEventLog://Application]
         index = endpoint
         disabled = false

         [WinEventLog://Security]
         index = endpoint
         disabled = false

         [WinEventLog://System]
         index = endpoint
         disabled = false

         [WinEventLog://Microsoft-Windows-Sysmon/Operational]
         index = endpoint
         disabled = false
         renderXml = true
         source = XmlWinEventLog:Microsoft-Windows-Sysmon/Operational

   and save the file to `C:\Program Files\SplunkUniversalForwarder\etc\system\local\` folder

   in the "Save as type" section, click text, and select "All Files, then in the "File name:" section, type "inputs.conf", and click "Save"
   
   2) hit the "Windows" key, type "services", right-click Services, and click "Run as administrator"
   3) scroll down and double-click on "SplunkForwarder"
   4) click the "Log On" tab, then click the "Local System account" radio button, click "Apply", then click "OK"
   5) right-click "SplunkFowarder", click "Restart", if you get a pop up saying that Windows could not stop the SplunkForwarder service, click "OK", then click "Start the service"

</details>

---

### 8) Continue Splunk Server configuration

<details>
<summary>Configuring Splunk Server to accept logs from the Windows Server 2022 (Active Directory Domain Controller) machine</summary>
<br>

   1) open a web browser, go to `192.168.10.10:8000`, and log into Splunk Server

If you configured the Windows 10 machine first, the configuration below has already been made. If not:
   
   2) at the top of the window, select "Settings", then select "Indexes"
   3) click "OK" then at the top-right, click "New Index"
   4) in the "Index Name" field, type in "endpoint", and click "Save"
   5) at the top of the window, click on "Settings", then click on "Forwarding and receiving"
   6) under "Received data", click on "Configuring receiving", click on "New Receiving Port", then type `9997` in the "Listen on this port" section, and click "Save"

If everything has been set up correctly up to this point, we should be receiving data from our Windows Server 2022 (Active Directory Domain Controller) into Splunk on our Ubuntu Server. To verify:

   1) click on "Apps" in the top-left corner, and click on "Search & Reporting"
   2) in the input field under "Search", type in `index=endpoint`, then click on the green magnifying glass search button
   3) on the left, under "SELECTED FIELDS", click the "a source" option

 If you see the following values:
 
    * WinEventLog:Security
    * WinEventLog:System
    * WinEventLog:Application
    * XmlWinEventLog:Microsoft-Windows-Sysmon/Operational

You have installed everything correctly.

</details>

---

### 9) Install and configure Windows Server

<details>
<summary></summary>
<br>

   1)

</details>

<!--

-->














<!--

left off at - Active Directory Project (Home Lab) | Part 3 - 26:17

<details>
<summary></summary>
<br>

   1)

</details>

-->

<!--
option 1

# PROJECTNAME

## Objective
[Brief Objective - Remove this afterwards]

### Skills Learned
[Bullet Points - Remove this afterwards]


### Tools Used
[Bullet Points - Remove this afterwards]

## Steps

-->

<!--

option 2

<h1>Project Name</h1>

 ### [YouTube Demonstration](https://)

<h2>Description</h2>

<br />

<h2>Languages and Utilities Used</h2>

- <b>language or utility</b> 

<h2>Environments Used </h2>

- <b>environment</b> (21H2)

<h2>Program walk-through:</h2>

<p align="center">
Launch the utility: <br/>
<img src="https://" height="80%" width="80%" alt="alt name"/>
<br />
<br />
Select the disk:  <br/>
<img src="https://" height="80%" width="80%" alt="alt name"/>
<br />
<br />
Enter the number of passes: <br/>
<img src="https://" height="80%" width="80%" alt="alt name"/>
<br />
<br />
Confirm your selection:  <br/>
<img src="https://" height="80%" width="80%" alt="alt name"/>
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://" height="80%" width="80%" alt="alt name"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://" height="80%" width="80%" alt="alt name"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://" height="80%" width="80%" alt="alt name"/>
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
