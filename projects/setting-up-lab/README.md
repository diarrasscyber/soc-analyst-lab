# 🛡️ SOC Analyst Home Lab – Full Setup Guide
This repository contains a complete step-by-step guide to building a SOC Analyst training lab, including Windows Server, Windows 10/11, Linux distributions, SIEMs, IDS/IPS, FTP server and web applications.

---

## 📑 Table of Contents
- [1. Installing the Lab Environment](#1-installing-the-lab-environment)
- [2. Installing & Configuring Windows Server 2022 (SIEM1)](#2-installing--configuring-windows-server-2022-siem1)
- [3.Confi guring Windows Server 2019](#3-configuring-windows-server-2019)
- [4. Installing Windows 10/11 VM](#4-installing-windows-1011-vm)
- [5. Installing Windows 10/11 VM (SIEM2)](#5-installing-windows-1011-vm-siem2)
- [6. Disable Internet Explorer Enhanced Security](#6-disable-internet-explorer-enhanced-security)
- [7. Adding Roles & Features on Windows Server 2019](#7-adding-roles--features-on-windows-server-2019)
- [8. Installing Parrot Security / Kali Linux](#8-installing-parrot-security--kali-linux)
- [9. Configuring OSSIM SIEM Server](#9-configuring-ossim-siem-server)
- [10. Disable Firewall & Defender on SIEM1](#10-disable-firewall--defender-on-siem1)
- [11. Share & Map SOC-Tools Directory](#11-share--map-soc-tools-directory)
- [12. Install Required Applications](#12-install-required-applications)
- [13. Create User Accounts (SIEM2)](#13-create-user-accounts-siem2)
- [14. Install SQL Server Express 2017](#14-install-sql-server-express-2017)
- [15. Test Network Connectivity](#15-test-network-connectivity)
- [16. Configure FTP Server (Server 2019)](#16-configure-ftp-server-server-2019)
- [17. Deploy LuxuryTreats Website](#17-deploy-luxurytreats-website)
- [18. Edit Hosts File (Windows & Linux)](#18-edit-hosts-file-windows--linux)

---

# 1. Installing the Lab Environment

### Install VMware or VirtualBox  
Configure the virtual network adapter:

1. Open **Edit → Virtual Network Editor**
2. Select **VMnet8**
3. Click **Change Settings**
4. Select VMnet8
5. Set IP address: `192.168.103.0/24`
 <img width="666" height="48" alt="image" src="https://github.com/user-attachments/assets/89cbd773-3eb7-4ea0-867f-0c28cc97f8ed" />
 
6. Open **NAT Settings**
   - Gateway IP: `192.168.103.1`
<img width="470" height="152" alt="image" src="https://github.com/user-attachments/assets/5bf8a927-eea0-4e4e-b587-6a7186979864" />
 
7. Open **DHCP Settings**
   - Start: `192.168.103.2`
   - End: `192.168.103.254`
<img width="363" height="199" alt="image" src="https://github.com/user-attachments/assets/051545bd-67b4-48b0-aaa8-8dbc48d4254a" />

8. Apply and confirm.

---

# 2. Installing & Configuring Windows Server 2022 (SIEM1)

### Install Windows Server 2022 VM
-install windows server 2022

### Rename the computer
- right click on the started menu
- system
- renamed this PC to 
- **SIEM1**

### Static IP Configuration
- IP: `192.168.103.22`
- Mask: `255.255.255.0`
- Gateway: `192.168.103.1`
- DNS: `8.8.8.8`
<img width="455" height="442" alt="image" src="https://github.com/user-attachments/assets/3fd8788a-f58b-410d-b515-31992c9552e9" />

Disable automatic Server Manager startup:
- Server Manager → Manage → Server Manager Properties

---

# 3. Configuring Windows Server 2019

### Install Windows Server 2019  
-install windows server 2019

### Rename the computer
- right click on the started menu
- system
- renamed this PC to 
- **windows19**

### Static IP
- IP: `192.168.103.19`
- Mask: `255.255.255.0`
- Gateway: `192.168.103.1`
- DNS: `8.8.8.8`

Disable automatic Server Manager startup:
- Server Manager → Manage → Server Manager Properties

---

# 4. Installing Windows 10/11 VM

- Add a second hard disk througt VMware
 <img width="381" height="316" alt="image" src="https://github.com/user-attachments/assets/2a7a2a8a-d447-4a16-a150-cc3e36c2918a" />

- Rename machine (Win10 or Win11)
- Assign static IP: `192.168.103.11`
- Create new disk volume:
  Windows + X → Disk Management → Create New Simple Volume

---

# 5. Installing Windows 10/11 VM (SIEM2)

- Create new VM  and install windows 10 or 11
- Rename → **SIEM2**
- Assign static IP: `192.168.103.18`

---

# 6. Disable Internet Explorer Enhanced Security

On **Server 2022 and 2019**:
- Server Manager → Local Server → IE Enhanced Security Configuration  
Disable for:
- Administrators  
- Users  

---

# 7. Adding Roles & Features on Windows Server 2019

Open:
**Server Manager → Add Roles and Features**

Enable:

- Web Server IIS  
- BranchCache  
- NFS Client  
- .NET Framework 3.5 (HTTP Activation, Non-HTTP Activation)  
- .NET Framework 4.7 (TCP Activation, Named Pipes)  
- SNMP Service  
- Telnet Client  
- TFTP Client  
- RPC over HTTP Proxy  
- FTP Server  

When prompted for installation source:
- at the specifying another source path, open a file explorer, click on This PC, open the Windows Server 2019 installation DVD, enter the SOURCES folder, then SXS and copy the link **DVD → sources/SXS**

Restart.

---

# 8. Installing Parrot Security / Kali Linux

- Install ParrotOS or Kali Linux  
- Run `ifconfig` to view interface name  
- Assign static IP: `192.168.103.13`
  <img width="700" height="354" alt="image" src="https://github.com/user-attachments/assets/6109c84e-c42e-464d-a866-b246bffd2094" />

- Reboot using `reboot` on the terminal

---

# 9. Configuring OSSIM SIEM Server

### VM Specs
- RAM: 8 GB  
- CPU: 4  
- Cores: 2  
- Disk: 60 GB  

Install:
- AlienVault USM OSSIM 4.13

### Assign IP
- `192.168.103.17`

### Default Login
- User: `root`
- Password: `toor`

### Network Configuration
- SENSOR → NETWORK CIDR → `192.168.103.0/24`

---

# 10. Disable Firewall & Defender Antivirus on SIEM1(windows server 2022)

### Firewall
- Control Panel → Windows Defender Firewall → Turn Off  
- Advanced Settings → Disable Domain Profile

### Disable Windows Defender Antivirus
Run:
`gpedit.msc`

Navigate:
- Computer Config → Admin Templates → Windows Components → Windows Defender Antivirus  
Enable:
- **Turn off Windows Defender Antivirus**

---

# 11. Share & Map SOC-Tools Directory (SIEM1:(windows server 2022))

On **SIEM1**:

1. Install WinRAR  
2. Shrink C: by 40GB → Create new partition  
3. Create folder: **SOC**
4. Extract SOC tools into SOC folder  
5. Enable Network Discovery  
6. Share folder → Permissions → Everyone = Read/Write  

On all machines (Win10, Win11, Server2019, SIEM2, kali linux):
- Map drive:
- that will allow to get access on the drive througt all machines

---

# 12. Install Required Applications

## ✔️ On SIEM1(windows server 2022):
- JDK  
- Notepad++  
- Google Chrome  
- Mozilla Firefox  
- WinPcap  
- Splunk Enterprise  

## ✔️ On Windows Server 2019(windows19):
- JDK  
- Notepad++  
- Google Chrome  
- Mozilla Firefox  
- WinPcap  

## ✔️ On Windows 10:
- JDK  
- Notepad++  
- Google Chrome  
- Mozilla Firefox  
- WinPcap  
- FileZilla  

## ✔️ On SIEM2(windows 10 or 11):
- JDK  
- Notepad++  
- Google Chrome  
- Mozilla Firefox  
- WinPcap  

---

# 13. Create User Accounts (SIEM2)

Create the following users:

-	Control Panel → Add User → Create accounts Martin, Jason, Shiela
-	Make Jason an Administrator

 **Martin**  
 **Jason** → *Administrator*  
 **Shiela**

---

# 14. Install SQL Server Express 2017

### Steps:
1. Install **SQL Server 2017 Express**  
2. Choose **Custom Installation**  
3. Select **all features**, except *Machine Learning Services*  
4. Go to **Database Engine Configuration** → select **Mixed Mode** → set admin password  
5. Install **SQL Server Management Studio (SSMS)**  
6. Restart the VM and connect to SQL Server  

---

# 15. Test Network Connectivity

Run ping commands between all machines to ensure communication:

ping 192.168.103.22
ping 192.168.103.19
ping 192.168.103.11
ping 192.168.103.13
ping 192.168.103.18

# 16. Configure FTP Server (Windows Server 2019)

Open: **IIS Manager → Sites → Add FTP Site**

### FTP Configuration
- **Name:** `demoFTPsite`
- **Path:** `C:\FTP`
- **IP:** `192.168.103.19`
- **Port:** `21`
- **SSL:** None
- **Authentication:** Basic  
- **Authorization:** All Users → Read/Write

---

# 17. Deploy LuxuryTreats Website on Windows Server 2019

Open: **IIS Manager → Sites → add new website

## WEB SITE Configuration
- Extract Project Files
Extract the **LuxuryTreats** folder.
- Copy LuxuryTreats Website Files
Copy the luxurytreat folder and paste it in the C drive: in inetpub folder then wwwroot C:\inetpub\wwwroot\LuxuryTreats
- Edit the *web.config* File with Notepad++ finding on C:\inetpub\wwwroot\LuxuryTreats
- At line 31 delete (providerName="System.Data.SqlClient")
- At the same line 31 replace windowsserver2012 with the name of our machine: windows19\SQLEXPRESS then save and close

- Open SQL Server management studio then click connect
- In the left pane right click on database then new database
- At database name level enter: hotels 
- Then in the left-handed pane click on option and ensure that at the recorvery model level choose simple then ok 
- We should see the hotel database when we expand DATABASE in the left pane
- In the lab prerequisite folder → website folder → DBscript folder → edit the scrip file with notepad++
- ctrl+A then ctrl+C to copy the contents of the script file
- Return to sql server management studio → select the HOTELS database → click on new query → paste the content of the script → execute to create the tables 
- Start menu → administration tool → IIS internet service manager → in the left pane expand windows19 → right click on site → add a website
- In the website name field: LuxuryTreats
- Physical path: choose drive c:(C:\inetpub\wwwroot\LuxuryTreats)
- IP address choose the address of the machine port 80
- Host name: www.luxurytreats.com → click ok

# 18. Configure Hosts File on all Windows & Linux 

## Windows
Edit the hosts file:
-	Edit: C:\Windows\System32\drivers\etc\hosts with notepad++ and add:
192.168.103.19   www.luxurytreats.com
127.0.0.1        fonts.googleapis.com
<img width="768" height="196" alt="image" src="https://github.com/user-attachments/assets/0a55c0e2-5970-4afa-8c65-16fb2fe3d1ee" />

## Kali/Parrot:
•	Edit /etc/hosts with nano or vim
•	Add the same entries
<img width="665" height="86" alt="image" src="https://github.com/user-attachments/assets/009c43c6-23f6-4234-8fcf-f1c6c2d9be8e" />

Open browser → Visit www.luxurytreats.com


