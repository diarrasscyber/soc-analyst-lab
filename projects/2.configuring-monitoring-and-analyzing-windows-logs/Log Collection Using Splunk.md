# 📊 Log Collection Using Splunk — Complete Lab Guide

The goal of this lab is to learn how to configure, collect, visualize, and analyze logs from different systems using Splunk Enterprise.
Splunk will allow us to: centralize logs from all machines on the network, analyze events, detect anomalies and cyberattacks.

## Environment — Virtual Machines Used

**Windows Server 2022 (SIEM1)** ➝ Will run Splunk Enterprise

**Windows Server 2019** ➝ Will run Splunk Universal Forwarder

**Windows 10** ➝ Will run Splunk Universal Forwarder

**Ubuntu (SNORT machine)** ➝ Will run Splunk Universal Forwarder

**Kali Linux** ➝ Attacker machine to generate malicious activity

---

# 1️⃣ Install Splunk Universal Forwarder on Windows Server 2019

-On Windows Server 2019, go to the SOC shared folder or download the Splunk Universal Forwarder

-Launch the installer

-Check the box: Accept the license agreement

-Click Customize Options

-Click Next, Next, Next

-Check all boxes under:

-Windows Event Logs

  Performance Monitor
  then click Next

-Leave the Deployment Server field empty.

-Enter the IP address of the Splunk Enterprise server (SIEM1):192.168.103.22:9997

# 2️⃣ Configure Splunk Universal Forwarder (Windows Server 2019)

Since the web server (IIS) is running on this machine, we must configure specific Splunk settings.

1. Copy default configuration files

Go to: C:\Program Files\SplunkUniversalForwarder\etc\system\default

Copy the following files:

**inputs.conf**
**props.conf**
**transforms.conf**

Paste them into: C:\Program Files\SplunkUniversalForwarder\etc\system\local

2. Modify the configuration files
   
 ## Edit inputs.conf

Open the file located in system\local

Delete all existing content

Copy and paste this part content from
“Config File 1 — Module 3 script” (from the shared SOC folder) to
C:\Program Files\SplunkUniversalForwarder\etc\system\local\inputs.conf

<img width="675" height="244" alt="image" src="https://github.com/user-attachments/assets/b92bee49-7066-4415-b596-1ea0c9293e42" />


## Configure outputs.conf

In the same Config File 1 (Module 3),
copy the corresponding output configuration section.

Paste it into the outputs.conf file located at:C:\Program Files\SplunkUniversalForwarder\etc\system\local\outputs.conf

<img width="678" height="250" alt="image" src="https://github.com/user-attachments/assets/42495521-0fb8-4202-a347-569b607fdacf" />

## Configure props.conf

Open the file:

C:\Program Files\SplunkUniversalForwarder\etc\system\local\props.conf

Delete all existing content.

Copy the props.conf section from
Config File 1 (Module 3 script) located in the shared SOC folder.

Paste it into the local props.conf file

<img width="588" height="209" alt="image" src="https://github.com/user-attachments/assets/69160d4a-bc9d-4e9e-bcbb-ce7fddc28da7" />


## Configure transforms.conf

Open the file:

C:\Program Files\SplunkUniversalForwarder\etc\system\local\transforms.conf

Delete all existing content.

Copy the transforms.conf section from
Config File 1 (Module 3 script) in the shared SOC folder.

Paste it into the local file

<img width="816" height="502" alt="image" src="https://github.com/user-attachments/assets/77bf1f6c-7a58-4b0c-a6ed-60f0db899f4b" />

## Restart the Splunk Forwarder Service

Press Windows + R

Type:services.msc

Press Enter to open the Services console.

Look for: SplunkForwarder Service

Right-click → Restart

<img width="945" height="257" alt="image" src="https://github.com/user-attachments/assets/7aa40f2a-799d-444b-853c-a67043a71a29" />



