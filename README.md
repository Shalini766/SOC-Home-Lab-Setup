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

