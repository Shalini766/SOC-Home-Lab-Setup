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
- To log in to the Kali machine, enter the default credentials "username=kali,password=kali"

### Step 4: Install Sysmon on Windows 10 VM
- Once the test machine is running, open a web browser and go to https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon
- Download Sysmon from Microsoft Sysinternals and extract it to a folder.
- Download the configuration file from https://github.com/olafhartong/sysmon-modular/blob/master/sysmonconfig.xml
- Open the PowerShell, run as an administrator.
- To be in the same folder, copy the folder path and paste it into PowerShell.
- Install using the below command

        .\Sysmon64.exe -i .\sysmonconfig.xml
### Step 5: Install Splunk Enterprise on Windows 10 VM











