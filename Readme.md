## **🛡️ Enterprise EDR \& Threat Hunting Grid — Sentient Shield**



#### Project Overview



This project focuses on building a Security Operations Center (SOC) environment using an Enterprise Endpoint Detection and Response (EDR) architecture. The goal is to monitor endpoints in real time, detect suspicious activities, and map security events for threat hunting and incident response.



The system is designed to simulate a real enterprise monitoring environment where endpoints continuously send telemetry data to a centralized security platform.



###### **✅ Week 1 — Infrastructure \& Agent Deployment**



Objective:



To design and deploy the foundational SOC infrastructure by setting up the Wazuh platform and onboarding a monitored endpoint into the environment.



**🧠 Architecture Setup**



A virtualized lab environment was created using Oracle VirtualBox consisting of:



Component	                   Role

Ubuntu Server	         Wazuh Manager + Dashboard (SOC Server)

Windows 10	         Monitored Endpoint

Internal Network	 Isolated SOC communication network



Network Design

An isolated internal network was configured to simulate enterprise segmentation:



Wazuh Server (Ubuntu): **192.168.100.10**



Windows Endpoint: **192.168.100.20**



This setup ensures secure communication between monitored endpoints and the SOC server without external network dependency.



**⚙️ Wazuh Deployment (SOC Server)**



The Wazuh platform was installed in All-in-One mode, which includes:



* Wazuh Manager (event processing)
* Wazuh Indexer (log storage \& search engine)
* Wazuh Dashboard (visual monitoring interface)



Key Tasks Performed

* Installed Wazuh on Ubuntu Linux.



Configured required services:



* wazuh-manager
* wazuh-indexer
* wazuh-dashboard



Verified service health using systemd.



Accessed dashboard securely via HTTPS.



Dashboard access: https://192.168.100.10



**🖥️ Endpoint Preparation (Windows 10)**



A Windows 10 virtual machine was deployed to act as an enterprise endpoint.



Configuration Steps

Installed Windows OS in VirtualBox.

Configured internal network adapter.

Assigned static IP address manually.

Installed VirtualBox Guest Additions for system integration.



**🔐 Wazuh Agent Deployment**



The Wazuh Agent was installed on the Windows endpoint to enable continuous monitoring.

Enrollment Process

Agent installed on Windows machine.

Agent registered on Wazuh server using manage\_agents.

Authentication key generated and imported.

Secure communication established between endpoint and server.

Agent service started successfully.



✅ **Verification**



The deployment was validated through the Wazuh Dashboard:

Endpoint successfully registered.

Agent status displayed as Active.

Telemetry communication confirmed.



Dashboard View:



Agents → Summary → win10-agent (Active)



**🎯 Outcome of Week 1**



By the end of Week 1:

A functional SOC infrastructure was established.

Endpoint monitoring capability was enabled.

Secure agent enrollment workflow was implemented.

Real-time event collection pipeline became operational.

This completed the foundational stage required for implementing detection logic and threat hunting capabilities in subsequent phases.



**📊 Current Architecture**

Windows Endpoint

&nbsp;       ↓

&nbsp;  Wazuh Agent

&nbsp;       ↓

&nbsp;  Wazuh Manager

&nbsp;       ↓

&nbsp;  Wazuh Indexer

&nbsp;       ↓

&nbsp;  Wazuh Dashboard

