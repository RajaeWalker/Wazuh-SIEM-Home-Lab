# Wazuh SIEM Home Lab with Sysmon Integration

## Project Overview

This project documents the design, deployment, and validation of a Security Information and Event Management (SIEM) home lab using Wazuh and Microsoft Sysmon. The lab was built in VMware Workstation with an Ubuntu Server hosting the Wazuh Manager, Indexer, and Dashboard, and a Windows 11 endpoint configured with the Wazuh Agent and Sysmon.

The goal of the project was to gain hands-on experience deploying a SIEM, collecting Windows security telemetry, creating custom detection rules, and investigating alerts through the Wazuh Dashboard. Throughout the project, I configured secure log collection, validated end-to-end event ingestion, and documented the environment to demonstrate practical SOC analyst skills.

## Objectives

- Deploy a Wazuh SIEM environment on Ubuntu Server.
- Configure a Windows 11 endpoint with the Wazuh Agent.
- Install and configure Microsoft Sysmon for enhanced event logging.
- Collect and analyze Windows Security and Sysmon events.
- Create and validate a custom Wazuh detection rule.
- Map detections to the MITRE ATT&CK framework.
- Develop practical skills in security monitoring, log analysis, and SIEM administration.
- Document the project for a professional cybersecurity portfolio.

- ## Technologies Used

| Technology | Purpose |
|------------|---------|
| Wazuh | Security Information and Event Management (SIEM) platform |
| Ubuntu Server | Hosts the Wazuh Manager, Indexer, and Dashboard |
| Windows 11 | Monitored endpoint |
| Microsoft Sysmon | Enhanced Windows event logging |
| Wazuh Agent | Collects endpoint logs and securely forwards them to the Wazuh Manager |
| VMware Workstation Pro | Virtualization platform |
| ossec.conf | Configured the Wazuh Agent to collect Sysmon event logs |
| MITRE ATT&CK Framework | Threat classification and mapping |
| GitHub | Project documentation and version control |

## Lab Environment

The lab was built in VMware Workstation Pro using two virtual machines connected through a private virtual network.

| Virtual Machine | Operating System | IP Address | Role |
|----------------|------------------|------------|------|
| Wazuh Server | Ubuntu Server | 192.168.74.128 | Hosts the Wazuh Manager, Indexer, and Dashboard |
| Windows Endpoint | Windows 11 | 192.168.74.129 | Generates Windows and Sysmon events that are collected by the Wazuh Agent |

## Network Communication

The lab used Wazuh's default communication ports to securely register the Windows endpoint, forward security events to the Wazuh server, and provide encrypted access to the web dashboard.

| Port | Purpose |
|------|---------|
| TCP 1514 | Secure transmission of Windows Event Logs and Sysmon events from the Wazuh Agent to the Wazuh Manager |
| TCP 1515 | Registers the Windows endpoint with the Wazuh Manager during agent enrollment |
| TCP 443 | Secure HTTPS access to the Wazuh Dashboard for monitoring alerts and events |

## Lab Workflow

The following workflow illustrates how security events are collected, processed, and analyzed within the Wazuh lab environment.

### 1. Generate Endpoint Activity
The Windows 11 endpoint generates normal operating system events through user activity, application execution, file creation, and system processes. Sysmon extends native Windows logging by recording detailed security telemetry such as process creation, file creation, network connections, and registry modifications.

### 2. Collect Security Events
The Wazuh Agent monitors both Windows Event Logs and the Sysmon Operational log. These events are collected in real time and prepared for secure transmission to the Wazuh Manager.

### 3. Secure Event Transmission
The Wazuh Agent securely forwards collected events to the Wazuh Manager using TCP port 1514. During the initial deployment, the Windows endpoint registers with the Wazuh Manager over TCP port 1515 before event collection begins.

### 4. Event Analysis
The Wazuh Manager normalizes incoming events and evaluates them against built-in detection rules. Matching events generate alerts with severity levels and MITRE ATT&CK technique mappings when applicable.

### 5. Alert Indexing
Processed alerts are stored by the Wazuh Indexer, enabling fast searching, filtering, and historical analysis of security events.

### 6. Security Monitoring
The Wazuh Dashboard retrieves indexed data and presents alerts, dashboards, MITRE ATT&CK mappings, and endpoint activity through a centralized web interface accessed over HTTPS (TCP 443).

### 7. Detection Validation
To validate the deployment, Sysmon events were successfully collected from the Windows endpoint and displayed within the Wazuh Dashboard, confirming that the agent, manager, indexer, and dashboard were functioning correctly.
