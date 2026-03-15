## **🛡️ Wazuh SIEM Home Lab for Threat Detection and Security Monitoring**

#### 

#### 📌 Project Overview



This project focuses on building a Security Operations Center (SOC) monitoring environment using an Enterprise Endpoint Detection and Response (EDR) architecture.



The goal is to monitor endpoints in real time, detect suspicious activity, and analyze security events for threat hunting and incident response.



The lab simulates a real-world enterprise monitoring environment where endpoints continuously send telemetry data to a centralized Wazuh SIEM platform.



The objective is to integrate a Windows endpoint with a centralized Wazuh server to collect logs, monitor system activity, and detect potential security threats.



**🎯 Project Goals**



Deploy Wazuh SIEM on Ubuntu Server



Configure secure dashboard access



Connect Windows endpoint using Wazuh Agent



Establish centralized log monitoring



Build a foundation for threat detection and analysis



🏗️ Lab Architecture

Windows 10 Endpoint (Wazuh Agent)

        │

        │ Logs \& Events

        ▼

Ubuntu Server (Wazuh Manager + Indexer + Dashboard)



🧰 Technologies Used



Wazuh 4.7.5

Ubuntu Linux

Windows 10 VM

VirtualBox

OpenSearch (Wazuh Indexer)



Filebeat



#### **📅 Week 1 — SIEM Deployment \& Agent Integration**



Tasks Completed



Installed Wazuh all-in-one deployment



Configured Wazuh Dashboard



Established internal VM network



Installed Wazuh agent on Windows endpoint



Registered and authenticated the agent



Verified communication between endpoint and SIEM



🌐 Network Configuration

Machine	Role	IP Address

Ubuntu VM	Wazuh Server	192.168.100.10

Windows VM	Endpoint Agent	192.168.100.20



**✅ Week 1 Outcome**



Functional SIEM environment deployed



Endpoint successfully onboarded



Real-time monitoring established



Lab ready for advanced telemetry collection



#### **📅 Week 2 — Endpoint Telemetry with Sysmon**



**Objective**



The objective of Week 2 was to enhance endpoint visibility by deploying Sysmon (System Monitor) on the Windows endpoint and integrating its telemetry with the Wazuh SIEM platform.



Sysmon provides detailed logging of system activities such as process execution, network connections, and file modifications, enabling deeper security monitoring within the SOC lab environment.



**Sysmon Installation**



Sysmon from the Microsoft Sysinternals Suite was installed on the Windows endpoint.



Installation command:



Sysmon64.exe -i -accepteula



Verification command:



Get-Service sysmon64



Expected output:



Status : Running



This confirms that the Sysmon service is successfully installed and active on the Windows system.



Sysmon Configuration Deployment



To enable advanced monitoring capabilities, the SwiftOnSecurity Sysmon configuration was applied.



Command used:



Sysmon64.exe -c sysmonconfig-export.xml



Successful output:



Configuration file validated

Configuration updated

Sysmon Event Logging



After configuration, Sysmon records detailed system activity within Windows Event Viewer.



**Event location:**



Event Viewer

→ Applications and Services Logs

→ Microsoft

→ Windows

→ Sysmon

→ Operational



Examples of monitored activities include:



Process creation



Command-line execution



Network connections



File creation events



Registry modifications



Persistence techniques



Suspicious system activity



Integration with Wazuh SIEM



The Wazuh agent installed on the Windows endpoint continuously monitors Windows Event Logs, including Sysmon events.



These logs are forwarded to the Wazuh server running on Ubuntu, where they are indexed and visualized in the dashboard.



**Event pipeline:**



Windows Endpoint

      ↓

Sysmon Event Logging

      ↓

Windows Event Logs

      ↓

Wazuh Agent

      ↓

Wazuh Manager

      ↓

Wazuh Indexer (OpenSearch)

      ↓

Wazuh Dashboard



**Security Events in Wazuh**



After integrating Sysmon, security events generated on the Windows system began appearing in the Wazuh dashboard.



Events can be viewed in:



Modules → Security Events



Observed events included:



Windows service configuration changes



Authentication activity



System process events



Windows database recovery operations



These alerts are automatically correlated with MITRE ATT\&CK techniques, providing context for potential attacker behaviors.



**✅ Week 2 Outcome**



Deployment of Sysmon for advanced endpoint telemetry



Integration of Sysmon logs with Wazuh SIEM



Centralized security event monitoring



Visualization of endpoint activity through the Wazuh dashboard



Initial MITRE ATT\&CK mapping of detected events



This setup provides the foundation for threat simulation and attack detection activities in Week 3.



#### **📅 Week 3 — Brute Force Detection \& Active Response Exploration**



**Objective**



The objective of Week 3 was to simulate a credential brute-force attack on the Windows endpoint and observe how Wazuh detects suspicious authentication activity using its built-in correlation rules.



This phase focuses on security event detection and SOC monitoring, validating that the SIEM platform can identify malicious login patterns.



**Configuration**



Active Response functionality within Wazuh was explored by updating the Wazuh manager configuration file:



/var/ossec/etc/ossec.conf



**Example configuration:**



<command>

  <name>firewall-drop</name>

  <executable>firewall-drop</executable>

  <timeout\_allowed>yes</timeout\_allowed>

</command>



<active-response>

  <command>firewall-drop</command>

  <location>local</location>

  <rules\_id>60204</rules\_id>

  <timeout>600</timeout>

</active-response>



After updating the configuration, the Wazuh manager service was restarted:



sudo systemctl restart wazuh-manager



**Attack Simulation**



A brute-force authentication scenario was simulated on the Windows endpoint by generating multiple failed login attempts.



**Command used:**



runas /user:FakeUser cmd



Incorrect credentials were entered repeatedly to produce authentication failure events in Windows logs.



Detection in Wazuh



Wazuh successfully detected the suspicious login activity and generated security alerts.



Field	                               Value

Rule ID	                               60204

Description	                 Multiple Windows logon failures

Alert Level	                        10

MITRE Technique	                       T1110



These alerts indicate that Wazuh identified repeated authentication failures commonly associated with brute-force attacks.



MITRE ATT\&CK Mapping



The detected activity was mapped to the MITRE ATT\&CK framework:



T1110 — Brute Force



**Tactic category:**



Credential Access

Security Monitoring



**The Wazuh dashboard provided visibility into:**



authentication failure alerts



attack technique classification



alert severity levels



endpoint activity timeline



These features allow SOC analysts to quickly identify abnormal behavior and investigate security incidents.



**Active Response Note**



In this lab environment, the attack originated from the same Windows endpoint being monitored.

Because of this, Wazuh did not execute the firewall blocking action to avoid interrupting communication between the agent and the manager.



However, the detection and alert generation worked correctly, demonstrating Wazuh’s capability to detect brute-force activity.



✅ Week 3 Outcome



Task	                                                        Status



Brute Force Attack Simulation	                            ✅ Completed

Authentication Failure Detection	                        ✅ Completed

Wazuh Alert Generation	                                  ✅ Completed

MITRE ATT\&CK Mapping	                                    ✅ Completed



Week 3 successfully demonstrated how Wazuh detects credential-based attacks and generates actionable security alerts within a SOC monitoring environment.







#### **📅 Week 4 — Threat Simulation \& Detection Analysis**

**🎯 Objective**



The objective of Week 4 was to simulate real-world adversary techniques on the monitored Windows endpoint and observe how the Wazuh SIEM platform detects and classifies malicious activity.



This stage focuses on threat simulation and security event analysis, demonstrating how security monitoring systems detect suspicious commands and map them to the MITRE ATT\&CK framework.



**⚔️ Attack Simulation**



Several commands commonly used by attackers were executed on the Windows endpoint to simulate malicious activity.



**PowerShell Command Execution**

* powershell -ExecutionPolicy Bypass -Command "whoami"



This command simulates suspicious PowerShell execution often used in post-exploitation activities.



**Account Discovery**

* net user



This command enumerates user accounts on the system, which attackers commonly perform during the reconnaissance phase of an intrusion.



System Information Discovery

whoami



This command identifies the currently logged-in user and is frequently used by attackers to understand privilege levels.



**🔎 Detection in Wazuh**



After executing these commands, Wazuh generated security alerts within the dashboard indicating suspicious activity on the endpoint.



The alerts were visible in:



Modules → Security Events



Wazuh analyzed the collected logs and correlated them with known attack patterns.



🧠 MITRE ATT\&CK Mapping



The simulated attacker activities were mapped to the following MITRE ATT\&CK techniques:



Technique	                                               Description

T1059	                                     Command and Scripting Interpreter (PowerShell)

T1087	                                                 Account Discovery

T1082	                                           System Information Discovery

T1110	                                           Brute Force (Week 3 simulation)



These mappings provide security analysts with context about attacker behavior and tactics.



📊 Security Monitoring



The Wazuh dashboard visualized the generated alerts and provided insights into:



suspicious command execution



attacker discovery techniques



authentication failure events



alert severity levels



endpoint activity timeline



This enables analysts to quickly detect and investigate abnormal system activity.



🧪 Threat Simulation Workflow

Attacker Commands Executed

&nbsp;       ↓

Windows Event Logs Generated

&nbsp;       ↓

Wazuh Agent Collects Logs

&nbsp;       ↓

Wazuh Manager Processes Events

&nbsp;       ↓

Wazuh Indexer Stores Alerts

&nbsp;       ↓

Wazuh Dashboard Displays Security Events



This workflow demonstrates how endpoint telemetry flows through the SIEM platform to generate actionable security alerts.



✅ Week 4 Outcome

Task	                                                               Status

PowerShell Attack Simulation	                                   ✅ Completed

Discovery Command Execution	                                     ✅ Completed

Wazuh Alert Detection	                                           ✅ Completed

MITRE ATT\&CK Technique Mapping	                                 ✅ Completed



Week 4 successfully demonstrated how Wazuh detects attacker behaviors and correlates system activity with known adversary techniques.



#### **🏁 Project Conclusion**



This project successfully implemented a Security Operations Center (SOC) monitoring lab using the Wazuh SIEM platform.



Throughout the four-week process, the environment evolved from basic infrastructure deployment to advanced threat detection and attack simulation.



Key achievements of the project include:



* Deployment of a fully functional Wazuh SIEM environment



* Integration of a Windows endpoint with advanced telemetry using Sysmon



* Detection of suspicious activities through security event correlation



* Simulation of real attacker techniques to test monitoring capabilities



* Visualization of security alerts through the Wazuh dashboard



* Mapping of detected activities to the MITRE ATT\&CK framework



* This lab demonstrates how SIEM platforms assist security analysts in monitoring systems, detecting attacks, and investigating potential security incidents.



* The project provides practical experience with SOC workflows, endpoint monitoring, threat detection, and security event analysis, which are essential skills in modern cybersecurity operations.
