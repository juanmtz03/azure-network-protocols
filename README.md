<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark and experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>  

**Part 1:**  
- Create a Resource Group in Azure  
- Set up Azure Virtual Network and Subnets  
- Deploy Azure Virtual Machines (Windows and Linux [Ubuntu])  
  - Configure Azure Network Security Groups (Firewall Resource)  

**Part2:**


<h2>Actions and Observations</h2>

<p>
First, I created an Azure Tenant and Subscription in Azure. After logging into the Azure portal, the dashboard should appear with no existing Resource Groups.
</p>
<p>
<img src="https://github.com/user-attachments/assets/b473e66a-630e-4931-a4ee-96bf338519d1" height="80%" width="80%" alt="Part 1"/>
</p>

<h2>Conclusion:</h2>

<p>
In conclusion, we set up a Microsoft Azure tenant, created a subscription, and established a Resource Group. Within this setup, we configured a Virtual Network with a subnet and deployed two Virtual Machines—one running Windows and the other Linux—both connected to the same network. Finally, we analyzed the traffic between the two VMs to understand their communication and network behavior.
</p>
<p>
<img src="https://github.com/user-attachments/assets/0008c717-6b53-484e-add2-6b8e53a13cb6" height="80%" width="80%" alt="what we did"/>
</p>


<br />
