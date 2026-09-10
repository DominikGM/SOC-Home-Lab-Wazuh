# SOC Home Lab – Wazuh

## Overview

This project is a home SOC laboratory built to practice security monitoring,
log analysis, alert investigation and incident detection.

The laboratory was built using Oracle VirtualBox, Ubuntu, Windows and Wazuh.

## Lab Architecture

The lab consists of:

- Ubuntu 26.04.1 LTS – Wazuh Server, Indexer and Dashboard
- Windows – Wazuh Agent
- Oracle VirtualBox
- Isolated internal network – SOC-LAB

### Network

| Machine | Role | IP Address |
|---|---|---|
| Ubuntu | Wazuh Server + Dashboard | 192.168.100.10 |
| Windows | Wazuh Agent | 192.168.100.20 |

## Technologies

- Wazuh
- Wazuh Agent
- Windows Event Logs
- Windows Security Events
- SIEM
- Oracle VirtualBox
- Log Analysis

## Completed Tasks

- Installed and configured Ubuntu
- Configured an isolated SOC-LAB network
- Installed Wazuh Server, Indexer and Dashboard
- Installed Wazuh Agent on Windows
- Connected Windows Agent to Wazuh Server
- Verified that the agent is active
- Generated the first security event
- Investigated a Windows authentication failure
- Analyzed Windows Event ID 4625

## Incident 001 – Authentication Failure

### Description

The first security event detected in the laboratory was an unsuccessful
Windows authentication attempt.

### Detection

Wazuh detected the following event:

- Agent: Windows-SOC-LAB
- Agent IP: 192.168.100.20
- Event ID: 4625
- Rule ID: 60122
- Rule Level: 5
- Event: Logon Failure – Unknown user or bad password

### Investigation

The event indicated an unsuccessful authentication attempt against the
Administrator account.

Important event fields:

- Target username: Administrator
- Workstation: SOC-WINDOWS
- Logon type: 2
- Source IP: ::1
- Status: 0xc000006d
- Sub-status: 0xc0000064

The source address `::1` indicates that the authentication attempt
originated locally from the Windows machine.

### Analysis

The event represents a failed authentication attempt.

Because the source address was localhost (`::1`), this test did not indicate
a remote attack.

Wazuh successfully collected the Windows Security event, analyzed it using
its detection rules and displayed the resulting alert in the Wazuh Dashboard.

### SOC Workflow

Windows Event Log  
↓  
Wazuh Agent  
↓  
Wazuh Manager  
↓  
Detection Rule  
↓  
Wazuh Dashboard  
↓  
SOC Analyst Investigation

### Conclusion

This was the first successfully detected and investigated security event
in the SOC home lab.

The laboratory successfully demonstrated the collection of Windows security
logs, detection of an authentication failure and investigation of the
resulting Wazuh alert.
