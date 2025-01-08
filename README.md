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

<h2>Create our Resources</h2> 
<p>To start with this lab, you only need an Azure Tenant and Subscription. This means simply creating an Azure account and adding a payment method (don’t worry—you can use a free or pay-as-you-go plan). Once that’s set up, we’ll be creating some virtual machines to dive into the lab!</p>
<p>
<img src="https://github.com/user-attachments/assets/7a477b65-25c1-4577-a800-8d0dd4d0177c" height="80%" width="80%" alt="Part 1"/>
</p>

<ol>
  <li>Create a Resource Group</li>
  <p>
<img src="https://github.com/user-attachments/assets/c0ad3b2b-368e-4858-87b4-01aaf022b29d" height="80%" width="80%" alt="Lab 1"/>
</p>
<ol>
  <li>Create a Resource Group</li>
  <li>Create a Windows 10 Virtual Machine (VM)
    <ul>
      <li>While creating the VM, select the previously created Resource Group</li>
      <li>While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet</li>
    </ul>
  </li>
  <li>Create a Linux (Ubuntu) VM
    <ul>
      <li>While creating the VM, select the previously created Resource Group and Vnet</li>
    </ul>
  </li>
  <li>Observe Your Virtual Network within Network Watcher</li>
</ol>
<h2>Observe ICMP Traffic</h2>
<p>
First, I created an Azure Tenant and Subscription in Azure. After logging into the Azure portal, the dashboard should appear with no existing Resource Groups.
</p>
<p>
<img src="https://github.com/user-attachments/assets/b473e66a-630e-4931-a4ee-96bf338519d1" height="80%" width="80%" alt="Part 1"/>
</p>
<h2>Observe SSH Traffic</h2>
<p>
First, I created an Azure Tenant and Subscription in Azure. After logging into the Azure portal, the dashboard should appear with no existing Resource Groups.
</p>
<p>
<img src="https://github.com/user-attachments/assets/b473e66a-630e-4931-a4ee-96bf338519d1" height="80%" width="80%" alt="Part 1"/>
</p>
<h2>Observe DHCP Traffic</h2>
<p>
First, I created an Azure Tenant and Subscription in Azure. After logging into the Azure portal, the dashboard should appear with no existing Resource Groups.
</p>
<p>
<img src="https://github.com/user-attachments/assets/b473e66a-630e-4931-a4ee-96bf338519d1" height="80%" width="80%" alt="Part 1"/>
</p>
<h2>Observe DNS Traffic</h2>
<p>
First, I created an Azure Tenant and Subscription in Azure. After logging into the Azure portal, the dashboard should appear with no existing Resource Groups.
</p>
<p>
<img src="https://github.com/user-attachments/assets/b473e66a-630e-4931-a4ee-96bf338519d1" height="80%" width="80%" alt="Part 1"/>
</p>
<h2>Observe RDP Traffic</h2>
<p>
First, I created an Azure Tenant and Subscription in Azure. After logging into the Azure portal, the dashboard should appear with no existing Resource Groups.
</p>
<p>
<img src="https://github.com/user-attachments/assets/b473e66a-630e-4931-a4ee-96bf338519d1" height="80%" width="80%" alt="Part 1"/>
</p>
<h2>Lab Cleanup (DON’T FORGET THIS)</h2>
<ul>
  <li>Close your Remote Desktop connection</li>
  <li>Delete the Resource Group(s) created at the beginning of this lab</li>
  <li>Verify Resource Group Deletion</li>
</ul>

<h2>Conclusion:</h2>

<p>
In conclusion, we set up a Microsoft Azure tenant, created a subscription, and established a Resource Group. Within this setup, we configured a Virtual Network with a subnet and deployed two Virtual Machines—one running Windows and the other Linux—both connected to the same network. Finally, we analyzed the traffic between the two VMs to understand their communication and network behavior.
</p>
<p>
<img src="https://github.com/user-attachments/assets/0008c717-6b53-484e-add2-6b8e53a13cb6" height="80%" width="80%" alt="what we did"/>
</p>


<br />
