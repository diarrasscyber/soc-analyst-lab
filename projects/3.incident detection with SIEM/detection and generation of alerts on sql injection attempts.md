## Detection & Alerting for SQL Injection Attempts with Splunk

This lab demonstrates how to detect and generate alerts for SQL Injection attacks using IIS logs collected by Splunk

**1. Lab Requirements**

You will need the following virtual machines:

Windows Server 2022 (SIEM1) — Splunk Enterprise installed

Windows Server 2019 — IIS + LuxuryTreats web application

Kali Linux — Used as the attacking machine

**2. Access Splunk on SIEM1**

Log in to the SIEM1 machine

Open Splunk in your browser

Go to:

Apps → Search & Reporting

**3. Run the SQL Injection Detection Query**

Enter the following SPL query in the search bar:

host=Windows19 sourcetype=iis 
| eval cs_uri_query = urldecode(cs_uri_query) 
| regex cs_uri_query ="/(\%27)|(\')|(\-\-)|(\%23)|(#)/ix" 
| iplocation c_ip 
| table _time cs_uri_query cs_User_Agent c_ip

**4. Create an Alert**

Click Save As

Choose Alert

Configure:

Trigger condition: Number of results > 0

Alert type: Real-time or Scheduled

Save
<img width="945" height="427" alt="image" src="https://github.com/user-attachments/assets/d7b1ad19-ba78-4c1f-b613-d70b2afd81f0" />

<img width="945" height="415" alt="image" src="https://github.com/user-attachments/assets/50749551-68ce-45dc-aa75-577f4c864c84" />


**5. Perform SQL Injection from Kali Linux**

On the attacker machine:

Open a browser

Navigate to: www.luxurytreats.com

Log in with: Login: bob
Password: Passw0rd

Go to My Orders

Open ORD-001

In the URL bar, append the SQL injection payload: ' or 1=1;

This simulates a real SQL injection attempt

**6. Check Triggered Alerts in Splunk**

On SIEM1:

Open Splunk

Go to:

Activity → Triggered Alerts

You will now see the SQL Injection Alert triggered by the attack

<img width="945" height="173" alt="image" src="https://github.com/user-attachments/assets/4e47ec8c-f49f-4eb1-a180-c637256891b1" />



**7. Additional Detection Query for XSS/Script Injection**

To detect XSS attempts or script injections in IIS logs, use:

host=Windows19 sourcetype=iis "%3SCRIPT" OR "JAVASCRIPT" OR "Alert" OR "3C%2Fscript"



