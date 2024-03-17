# SOC Simulation in Microsoft Azure.

![Cloud Honeynet / SOC](https://github.com/Hammad-AlQuraishi/mediumImages/blob/main/SOC%20Simulation%20in%20Azure/Main%20diagram.jpg)

# Introduction

In this project, I build a self-contained simulation of an actual SOC in Microsoft Azure by creating some resources such as VMs, key vaults, storage, etc. I then configured their logs to flow into the Log Analytics Workspace which were utilized by Microsoft Sentinel (our SIEM in this case) to trigger incidents and alerts in case of breaches and disruptions in compliance. After having established the environment, I allowed it to run unhindered for 24 hours, wide open to the public internet with the bare minimum security. Thereafter, I collected and triaged some of the numerous incidents that occurred in that 24 hour period, and applied some hardening measures from NIST 800-43. I allowed the environment to run again for another 24 hours, this time much more secured with firewall configured and NIST 800-43's SC-7 applied. The statistics for both of these runs are compared and contrasted and they are presented below in a table format:

![statistics](https://github.com/Hammad-AlQuraishi/mediumImages/blob/main/SOC%20Simulation%20in%20Azure/statistics2.png?raw=true)

The statistical changes are measured below:
![summary of statistics](https://github.com/Hammad-AlQuraishi/mediumImages/blob/main/SOC%20Simulation%20in%20Azure/statistics3.png)


### Metrics utilized to determine the lack of security and security thereafter:
- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

### State of the environment before hardening:
![Environment before hardening](https://github.com/Hammad-AlQuraishi/mediumImages/blob/main/SOC%20Simulation%20in%20Azure/diagram%20before%20hardening.jpg)

### State of the environment after hardening:
![Environment after hardening](https://github.com/Hammad-AlQuraishi/mediumImages/blob/main/SOC%20Simulation%20in%20Azure/after%20hardening.jpg)

### Elements present in the environment:
- A Windows virtual machine.
- A Linux virtual machine.
- A key vault.
- A blob storage account.
- Log analytics workspace.
- Microsoft Sentinel.
- A Virtual network containing the VMs, the vault and the storage account.

Following below are the before and after snapshots for different resources present in the environment.

### Before snapshot for the Windows VM (mostly authentication attempts):
![Windows before hardening](https://github.com/Hammad-AlQuraishi/mediumImages/blob/main/SOC%20Simulation%20in%20Azure/Attacks%20on%20Windows%20before%20hardening.png)

### After snapshot for the Windows VM (mostly authentication attempts):
![Windows after hardening](https://github.com/Hammad-AlQuraishi/mediumImages/blob/main/SOC%20Simulation%20in%20Azure/Attacks%20on%20Windows%20after%20hardening.png)

### Means of hardening the Windows VM:
Primarily, it was configuring the right NSGs to allow for only the authenticated, mostly internal traffic to RDP into the machine. 
