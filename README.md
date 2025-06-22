# Setting-Up-a-Honeypot-in-Microsoft-Azure-to-Track-Attackers-Using-Geolocation

Ever wondered where cyber attackers are coming from? I set up a honeypot VM on Microsoft Azure, exposed it to attacks, and tracked the attackers using geolocation data.

In this lab, we will

- Deploy an Azure Virtual Machine as a honeypot
- Allow all inbound traffic to attract attackers
- Configure Log Analytics Workspace
- Set up Microsoft Sentinel to collect logs
- Querying failed login attempts 
- Extract failed RDP login attempts and attacker IPs
- Use a PowerShell script to get geolocation data
- Visualize attacker locations on a world map


## Step 1: Deploy the Honeypot Virtual Machine

To simulate a vulnerable system, I created an Azure Virtual Machine and i turned off the VM Firewall from the OS Level so as to enable attack access to the VM.

1️⃣ Create a Virtual Machine (VM) in Azure.
My machine 
•Name: UAT-server
•Resource Group: hugo-rg
•Specs: Standard B4as v2 (4 vcpus, 16 GiB memory)

![image1](https://github.com/user-attachments/assets/537e2bfe-5f7b-4b85-9237-ee37a9027caf)


2️⃣ Configure the Network Security Group (NSG):
•Go to Networking → Select Advanced → Create new NSG.
•Delete default inbound rules and create a new rule:
•Port: * (Allow all)
•Protocol: Any
•Action: Allow
•Priority: 200
•Rule Name: AllowAnyCustomAnyInbound

![image](https://github.com/user-attachments/assets/0590fcc7-c517-4efb-9f85-c21751abb682)

### Set Up Log Collection with Microsoft Sentinel

Now, we need to monitor incoming attacks using Microsoft Sentinel.

1️⃣ Create a Log Analytics Workspace (UAT-LogWorkSpace) to store and query logs.
2️⃣ Enable Microsoft Sentinel and link it to the workspace.

![image](https://github.com/user-attachments/assets/ff5f7dc8-c8e9-4bd7-adf6-adc79e979454)

![image](https://github.com/user-attachments/assets/e5b3123a-cddf-4d3f-b4dd-1ca2aedbbde0)


Installing the “Windows Security Events via AMA” Data Connector:
•Go to Data Connectors → Select Windows Security Events via AMA.
•Click Create New Data Collection Rule.
•Name: Windows Events, select the VM, and Connect.

📌 This allows Sentinel to collect login attempt data from the honeypot!

![image](https://github.com/user-attachments/assets/c22ba205-862f-4ce8-b6cf-fea84f622af7)

![image](https://github.com/user-attachments/assets/f8daf731-c996-452b-8574-ae05ee821c14)





