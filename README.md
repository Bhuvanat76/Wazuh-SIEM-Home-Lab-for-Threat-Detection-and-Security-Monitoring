### **🛡️ Enterprise EDR \& Threat Hunting Grid — Sentient Shield**

##### 📌 Project Overview



This project focuses on building a Security Operations Center (SOC) environment using an Enterprise Endpoint Detection and Response (EDR) architecture. The goal is to monitor endpoints in real time, detect suspicious activities, and map security events for threat hunting and incident response.

The system is designed to simulate a real enterprise monitoring environment where endpoints continuously send telemetry data to a centralized security platform.



This project demonstrates the deployment of a Security Information and Event Management (SIEM) environment using \*\*Wazuh\*\* to monitor endpoints and collect security telemetry.

The objective is to simulate a real-world SOC (Security Operations Center) setup by integrating a Windows endpoint with a centralized Wazuh server.



---



###### 🎯 Project Goals

\- Deploy Wazuh SIEM on Ubuntu Server

\- Configure secure dashboard access

\- Connect Windows endpoint using Wazuh Agent

\- Establish centralized log monitoring

\- Build a foundation for threat detection and analysis



---



###### 🏗️ Lab Architecture

Windows 10 Endpoint (Agent)

│

│ Logs \& Events

▼

Ubuntu Server (Wazuh Manager + Indexer + Dashboard)



---



###### 🧰 Technologies Used

\- Wazuh 4.7.5

\- Ubuntu Linux

\- Windows 10 VM

\- VirtualBox

\- OpenSearch (Wazuh Indexer)

\- Filebeat



---



###### **📅 Week 1 — SIEM Deployment \& Agent Integration**



✅ Tasks Completed

\- Installed Wazuh all-in-one deployment

\- Configured Wazuh Dashboard

\- Established internal VM network

\- Installed Wazuh agent on Windows endpoint

\- Registered and authenticated agent

\- Verified communication between endpoint and SIEM



---



###### 🌐 Network Configuration

| Machine | Role | IP Address |

|--------|------|------------|

| Ubuntu VM | Wazuh Server | 192.168.100.10 |

| Windows VM | Endpoint Agent | 192.168.100.20 |



---



###### 📸 Deployment Verification



\### Wazuh Dashboard Running

!\[Dashboard](screenshots/week1-dashboard.png)



\*Wazuh dashboard successfully deployed and accessible via HTTPS.\*



---



\### Agent Successfully Connected

!\[Agent Active](screenshots/week1-agent-active.png)



\*Windows endpoint registered and actively monitored.\*



---



\### Network Connectivity Validation

!\[Network](screenshots/week1-network-connectivity.png)



\*Successful communication between endpoint and SIEM server.\*



---



\## ✅ Week 1 Outcome

\- Functional SIEM environment deployed

\- Endpoint successfully onboarded

\- Real-time monitoring established

\- Lab ready for advanced telemetry collection



---







