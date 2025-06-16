# Building a SOC + Honeynet in Azure (Live Traffic)
![image](https://github.com/delvincybertech/Cloud-SOC/assets/164829222/1b766875-2b86-4b31-b473-26a53890fd20)


## Introduction

In this project, I constructed a miniature honeynet within the Azure environment. I collected log data from diverse sources and consolidated them into a Log Analytics workspace. This workspace serves as the foundation for Microsoft Sentinel, enabling the creation of attack visualizations, alert triggers, and incident management.

The process involved monitoring security metrics within the vulnerable environment over 24 hours. Subsequently, security measures were implemented to harden the environment. Following this enhancement, another 24-hour metric assessment was conducted. The results are outlined below. The metrics to be presented include:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 Windows, 1 Linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

In the "BEFORE" phase, all resources were initially deployed with direct exposure to the internet. The Virtual Machines had unrestricted Network Security Groups and open built-in firewalls, while other resources were configured with public endpoints accessible from the internet, rendering Private Endpoints unnecessary.

In contrast, the "AFTER" metrics reflect significant enhancements in security measures. Network Security Groups were strengthened by blocking all traffic except for access from my admin workstation. Additionally, all other resources were safeguarded by activating their built-in firewalls and implementing Private Endpoints.
## Attack Maps Before Hardening / Security Controls
![image](https://github.com/delvincybertech/Cloud-SOC/assets/164829222/a8dfdabc-ab95-418a-aa55-103c82131836)<br>
![image](https://github.com/delvincybertech/Cloud-SOC/assets/164829222/d783217a-7a0e-4faf-adcb-114c7d22364e)<br>
![image](https://github.com/delvincybertech/Cloud-SOC/assets/164829222/cb085e84-61af-45f0-9933-ccd6436e9ee4)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-03-21 20:37:05
Stop Time 2024-03-22 20:37:05

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 46,867
| Syslog                   | 23,181
| SecurityAlert            | 1
| SecurityIncident         | 191
| AzureNetworkAnalytics_CL | 2,718

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-03-24 00:22:02
Stop Time	2024-03-25 00:22:02

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 18,905
| Syslog                   | 1
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.
