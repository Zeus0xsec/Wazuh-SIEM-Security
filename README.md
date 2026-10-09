# 🛡️ Wazuh SIEM & Automated Alerting Pipeline

[![PL](https://img.shields.io/badge/Język-Polski-red.svg)](README_PL.md)
[![EN](https://img.shields.io/badge/Language-English-blue.svg)](README.md)

## 📌 Project Overview
This project focuses on deploying **Wazuh SIEM** to monitor a Windows Server Active Directory environment and configuring a secure, automated alerting pipeline using a local **Postfix** SMTP relay and **Mailtrap**.

## ⚙️ Technologies Used
* **SIEM:** Wazuh Manager & Wazuh Agent
* **OS:** Ubuntu Linux, Windows Server 2022
* **Networking:** VirtualBox Internal Network, Static Routing
* **Email Pipeline:** Postfix (SMTP Relay), SASL Authentication, Mailtrap

## 🚀 Key Features Configured
* Installed Wazuh Manager on an Ubuntu virtual machine and successfully linked a Wazuh Agent running on a Windows Server Domain Controller.
* Real-time monitoring of Windows Security Event Logs (focusing on AD User Management, e.g., Event ID 4720).
* Secure email delivery using Postfix as a relay host with SASL authentication to bypass external SMTP blocks.
* Custom alert thresholds mapped to automated email notifications via `ossec.conf`.

## 🛠️ Challenges & Troubleshooting (How I solved them)
1. **Postfix SASL Authentication Failure:** 
   * *Problem:* Postfix initially couldn't authenticate with the external Mailtrap sandbox, resulting in bounced alerts.
   * *Solution:* I carefully mapped the credentials in `/etc/postfix/sasl_passwd`, compiled the database using `postmap`, and enforced strict permissions (`chmod 600`) to secure the credentials before restarting the Postfix service.
2. **Wazuh Agent Connectivity Issues:** 
   * *Problem:* The Windows agent had a "Disconnected" status in the Wazuh dashboard.
   * *Solution:* I diagnosed a virtual routing issue. I enforced static IPs on the internal VirtualBox network (`192.168.10.x`) and restarted the agent via PowerShell (`Restart-Service -Name wazuh`), which established a stable connection.

## 📸 Screenshots
<img width="1710" height="1387" alt="Stan Wazuh" src="https://github.com/user-attachments/assets/045e3f98-0244-4665-a209-2b1ac128738d" />
<img width="1024" height="830" alt="Logi Wazuh" src="https://github.com/user-attachments/assets/a89b222c-c2d8-496e-bed0-9d3a588e8a0f" />
<img width="1715" height="1386" alt="Logi WS" src="https://github.com/user-attachments/assets/cf891df2-83ed-4f26-b6be-f57c57a1fcbd" />
<img width="1024" height="389" alt="MailTrap" src="https://github.com/user-attachments/assets/91dcf643-f9ac-4b3b-aeeb-a6ebb4427298" />
