# Building a SIEM

## Objective

The SIEM Building project aimed to create and configure a central platform to log and analyze security events on my virtual machine. The goal was to become familiar with how a SIEM works and all of its moving parts through a hands-on approach. This project introduced me to key components of a SIEM, including log analytics, data connectors, and queries.

### Skills Learned

- Advanced understanding of SIEM concepts and practical application.
- Real-time monitoring of events for anomolies or potential security incidents.
- Configuring data connectors to send data and event logs from VM to Log Analytics Workspace to SIEM for efficient event monitoring
- Creating query rules to specify what type of security events we want to be alerted of using KQL.
- Configuring VM firewall to allow traffic from more sources to generate more telemetry for testing purposes.

### Tools Used

- Microsoft Sentinel Security Information and Event Management (SIEM) system for log ingestion and analysis.
- Microsoft Azure for hosting my resource group, VMs, log analytics workspace, and SIEM dashboard.
- Windows Security Events data connectors to send data from VM via Azure Monitor Agent(AMA).

## Project Walkthrough
First, I set up a Windows 10 Pro Virtual Machine using Microsoft Azure. I intentionally left the RDP port open on this machine as to easily generate lots of network traffic. This way, my VM would act as a honeypot, attracting lots of attacks which I could then log and send to my SIEM later on.

*Ref 1: Virtual Machine with Open RDP Port*

<img width="800" alt="Screenshot 2025-01-17 at 6 45 51 PM" src="https://github.com/user-attachments/assets/06cedb04-e4f8-4cd7-9733-edf9e4851fde" />

Next, I created a Log Analytics workspace on Azure and deployed Microsoft Sentinel onto my workspace. Now, I have a workspace where I can pull event logs from my VM and then display them in a structured interface using Sentinel.

*Ref 2: SIEM Dashboard*

<img width="800" alt="Screenshot 2025-01-18 at 2 23 09 PM" src="https://github.com/user-attachments/assets/c3131dbc-2c06-4276-a7e8-d9cb3ae39d02" />

Next, I set up a data connector, which I would use to pull event logs from my VM and send them to my Log Analytics Workspace. I used the Windows Security Events data connector for my purposes.

*Ref 3: Data Connector Setup*

<img width="800" alt="Screenshot 2025-01-17 at 6 59 24 PM" src="https://github.com/user-attachments/assets/91966c67-2a29-4278-a0a6-94b951dfb5d9" />

Next, I created a query rule using KQL to check our event logs for successful sign-ins via RDP to our VM. This way, if our VM is attacked via RDP, we will be alerted on our SIEM. I set this to query every 5 minutes so we are always updated. I also added some other built-in rules.

*Ref 4: Query Rule*

<img width="800" alt="Screenshot 2025-01-17 at 7 04 13 PM" src="https://github.com/user-attachments/assets/1047c0ac-a436-4afb-8981-0f84bed98900" />

I let the machine run for a few day, and when I checked it, my SIEM had logged over 80,000 security events, including several incidents of successful log-ins and other alerts. I also logged the attackers' IP addresses, detecting attacks from countries such as Russia, India, and the Netherlands.

*Ref 5: SIEM Dashboard after 2 days*

<img width="800" alt="Screenshot 2025-01-20 at 1 26 56 AM" src="https://github.com/user-attachments/assets/e13ba04e-8c8f-4062-a42f-3ef86ec1e0f0" />



