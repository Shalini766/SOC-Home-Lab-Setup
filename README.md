# SOC-Home-Lab-Setup
This project is based on setting up a functional and isolated SOC home lab environment for cybersecurity learning and threat detection practice. This lab simulates attacker and defender roles using tools like Kali Linux (attacker), Windows + Sysmon (endpoint monitoring), and Splunk (log analysis and SIEM).

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

### Step 2: Creating Virtual Machines

#### Windows 10 VM:

- Install Windows 10 ISO

- Enable the network adapter in NAT/Host-only mode for isolation

#### Kali Linux VM:

- Download ISO from https://www.kali.org

- Basic setup with networking enabled

#### Install Sysmon on Windows 10

- Download Sysmon from Microsoft Sysinternals
- Open the command prompt, run as administrator, and install using the below command

        ** .\Sysmon64.exe -i .\sysmonconfig.xml **





