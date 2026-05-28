# Azure Sentinel SIEM Home Lab

## Objective 

The main focus of this project was to deploy a cloud-based SIEM environment using Microsoft Azure and Microsoft Sentinel to develop hands-on experience with Sentinel and to practice real-world threat detection, log analysis and attack visualisation via a geographical attack map

## Tools Used

- Microsoft Azure (VMs, VNets, Resource Groups and Log Analytics Workspace)
- Microsoft Sentinel (SIEM)
- Windows 11 (Honeypot VM)
- KQL (Kusto Query Language)
- Azure NSG (Network Security Group) for firewall rules

<img width="1900" height="766" alt="VM1" src="https://github.com/user-attachments/assets/44f4ff28-d63a-45dc-a0aa-6ebd25311f0f" />

## Overview

I intentionally created an exposed Windows 11 honeypot VM that generated security events, which I forwarded to LAW, had correlated and ingested by Sentinel, and queried with KGL using location and EventID data to detect brute-force attempts.

## What I did
- Deployed a Windows 11 VM with Defender disabled and created an inbound security rule titled DANGER-AllowAnyTraffic that permitted all inbound traffic to simulate a honeypot.
- Created a Log Analytics Workspace and connected it to Microsoft Sentinel
- Configured the Windows Security Events data connector and DCR
- Wrote various KQL queries to filter through failed brute force attacks (EventID 4625)
- Enriched the log data with geographical data using IP information and a custom watchlist
- Created a Sentinel Workbook attack map visualising real-world brute force attacks by source location 

<img width="1354" height="866" alt="SentinelDashboard" src="https://github.com/user-attachments/assets/589bf250-e02d-4dfd-8290-06e25b7b66db" />

## Key Findings

### Time to First Attack: Under 20 minutes
The VM began being exposed to the internet at 1300. Within 20 minutes, the first 4625 events were detected, perfectly demonstrating how quickly exposed, internet-facing systems are discovered and targeted.

### Attack Origin
The first 4 attempts were from Cape Town, South Africa. The attempts targeted the username 'AZUREUSER' and 'AZUREADMIN'. Based on research, this is a common default credential guess used by automated brute-force tools.

<img width="1043" height="635" alt="WindVM-Map-Day1" src="https://github.com/user-attachments/assets/6e660b30-d3c9-461e-b0bb-5069f5dcee42" />

## KQL Query Used

<img width="1084" height="800" alt="KQL-Query-Results" src="https://github.com/user-attachments/assets/6aea15cd-9932-4054-b0e1-4c22ed4bafc4" />
