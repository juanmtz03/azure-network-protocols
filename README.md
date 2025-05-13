<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark and experiment with Network Security Groups. <br />

<h2>Video Demonstration</h2>

- ### [YouTube: Creating some virtual machines to dive into the lab!](https://youtu.be/2_FNf9q3QTc)
 
<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<p>To start with this lab, you only need an Azure Tenant and Subscription. This means simply creating an Azure account and adding a payment method (don’t worry—you can use a free or pay-as-you-go plan). Once that’s set up, we’ll be creating some virtual machines to dive into the lab!</p>
<p>
<img src="https://github.com/user-attachments/assets/7a477b65-25c1-4577-a800-8d0dd4d0177c" height="80%" width="80%" alt="Part 1"/>
</p>

<p>
<ol>  
  <li>Create a Resource Group</li>
  
- After creating your resource group, click on it to access the page.
- Name the resource group “RG network activities.”
- Ensure the name matches the image provided for this lab.
- Click “Review and Create.”
- After validation passes, click “Create.”
- The resource group will be created in the Azure subscription in the “West US 2” location.
  
<img src="https://github.com/user-attachments/assets/9090ac41-13cf-41b8-a85c-5eb7cb1a0868" alt="Screen Shot 2025-01-07 at 21 35 08 PM" width="80%">
<img src="https://github.com/user-attachments/assets/8b7056ca-1e01-4e75-97c6-5870a18fbf64" alt="Screen Shot 2025-01-07 at 21 35 14 PM" width="80%">
<img src="https://github.com/user-attachments/assets/593b4c8b-88a7-4985-b807-06f7e5b71102" alt="Screen Shot 2025-01-07 at 21 36 15 PM" width="80%">
<img src="https://github.com/user-attachments/assets/01e8b90f-ec54-4f3b-8566-1d69ee2c87de" alt="Screen Shot 2025-01-07 at 21 36 30 PM" width="80%">
<img src="https://github.com/user-attachments/assets/fbd045e4-5aee-4504-914e-08cba88f0588" alt="Screen Shot 2025-01-07 at 21 36 36 PM" width="80%">
<img src="https://github.com/user-attachments/assets/e9b61cc5-6b13-48ec-ad4f-3ac484e169b8" alt="Screen Shot 2025-01-07 at 21 36 45 PM" width="80%">

 <li>Create a Windows 10 Virtual Machine (VM)</li>
 
- Search for “Virtual Machines” and select the “Virtual Machine” option.
-	Choose the first available virtual machine option.
-	Associate Virtual Machine with Resource Group: Select the previously created resource group (“RG network activities”).
-	If the resource group doesn’t appear, allow time for Azure Portal to finish creating it and then create the VM.
   
<img src="https://github.com/user-attachments/assets/15fd473e-4a76-4a75-ba9c-3123b9a80584" alt="Screen Shot 2025-01-07 at 21 37 17 PM" width="80%">
<img src="https://github.com/user-attachments/assets/9f8928da-17e2-4bde-a488-37b13908242d" alt="Screen Shot 2025-01-07 at 21 37 23 PM" width="80%">
<img src="https://github.com/user-attachments/assets/4a64ea01-8521-4530-9381-6465b61898a0" alt="Screen Shot 2025-01-07 at 21 37 28 PM" width="80%">
<img src="https://github.com/user-attachments/assets/b43edc4d-286b-42ea-9b50-77a76a4a95d7" alt="Screen Shot 2025-01-07 at 21 38 06 PM" width="80%">

  <li>While creating the VM, select the previously created Resource Group</li>
  
- Set Virtual Machine Details:
  - Name: windows-vm
  - Ensure the location is set to “West US 2” for consistency with the resource group.
  - Choose “Windows 10” as the OS.
  - For the size, select an option with at least 2 CPUs. You may choose up to 4 CPUs for a higher specification (estimated cost will be less than $10-20 a month, depending on usage).

- Set Username and Password:
  - Username: `labuser`
  - Password: `Cyberlab123!`

- Click "I confirm..." and "Next: Disk".
- Click "Next: Networking".
  
<img src="https://github.com/user-attachments/assets/2effb84f-6108-4991-81a7-8d9bde6d39ec" alt="Screen Shot 2025-01-07 at 21 38 54 PM" width="80%">
<img src="https://github.com/user-attachments/assets/05816298-2bbf-4fdf-b63a-1c9b3a5ea5f7" alt="Screen Shot 2025-01-07 at 21 39 06 PM" width="80%">
<img src="https://github.com/user-attachments/assets/e498f13d-e8f5-4dbb-9d72-c46f4d80586f" alt="Screen Shot 2025-01-07 at 21 39 16 PM" width="80%">
<img src="https://github.com/user-attachments/assets/503413d7-f9d1-427e-a434-3087b09207e5" alt="Screen Shot 2025-01-07 at 21 42 09 PM" width="80%">
<img src="https://github.com/user-attachments/assets/f5cfa6db-55f6-4038-ba54-36e65c80bc75" alt="Screen Shot 2025-01-07 at 21 42 18 PM" width="80%">
<img src="https://github.com/user-attachments/assets/b662d59d-04bd-40d3-8f16-97cccc522296" alt="Screen Shot 2025-01-07 at 21 43 27 PM" width="80%">

<li>While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet</li>
  
- Create a new virtual network and ensure the name matches the image provided for this lab.
- Confirm and click “OK.”

- Final Steps:
  - Click “Review and Create.”
  - If validation passes, click “Create.”
  - Wait for the deployment to complete. You’ll see a notification on the top right once it’s successfully deployed.
  - For safety, refresh the portal by typing “portal.azure.com” to ensure everything is correctly displayed and running.

 
<img src="https://github.com/user-attachments/assets/609ffc0b-c3c1-4e81-9e5e-ac43cad4c520" alt="Screen Shot 2025-01-07 at 21 43 35 PM" width="80%">   
<img src="https://github.com/user-attachments/assets/ef937194-c40f-4364-bbd5-30ff18094d1b" alt="Screen Shot 2025-01-07 at 21 43 38 PM" width="80%">
<img src="https://github.com/user-attachments/assets/e1d126db-ed89-4a09-9766-4f4d8bb3ddf8" alt="Screen Shot 2025-01-07 at 21 44 07 PM" width="80%">
<img src="https://github.com/user-attachments/assets/3460db73-5b8d-46d1-93fe-3a99b71e845f" alt="Screen Shot 2025-01-07 at 21 44 11 PM" width="80%">
<img src="https://github.com/user-attachments/assets/495bcbdf-39be-43b2-b1fe-b337acdebdcb" alt="Screen Shot 2025-01-07 at 21 44 19 PM" width="80%">
<img src="https://github.com/user-attachments/assets/7812d759-a0cf-400b-b9f0-396e0b2badbf" alt="Screen Shot 2025-01-07 at 21 46 00 PM" width="80%">
<img src="https://github.com/user-attachments/assets/af18c532-e446-4fc8-8977-9848e7b8fdc1" alt="Screen Shot 2025-01-07 at 21 46 29 PM" width="80%">
<img src="https://github.com/user-attachments/assets/813171c4-53e7-4089-b99f-5c9445c99565" alt="Screen Shot 2025-01-07 at 21 47 10 PM" width="80%">
<img src="https://github.com/user-attachments/assets/a2e083b9-dc6c-4ac1-8b86-df1ff61e6b73" alt="Screen Shot 2025-01-07 at 21 49 44 PM" width="80%">
<img src="https://github.com/user-attachments/assets/6f2e7798-c216-4a89-b024-69ff701c5eb3" alt="Screen Shot 2025-01-07 at 21 50 01 PM" width="80%">
<img src="https://github.com/user-attachments/assets/8261542b-ca0d-4c2b-80ab-b4f8e4ba6e5c" alt="Screen Shot 2025-01-07 at 21 50 16 PM" width="80%">

<li>Create a Linux (Ubuntu) VM
</li>

-While creating the VM, select the previously created Resource Group  
  - Name the virtual machine: `linux-vm`.  
  - Ensure the location is set to the same region as the Windows VM: West US 2 (to allow connectivity between the VMs).  
  - For the image, select Ubuntu Server 24, Gen 2.  
  - For the size, choose an option with 2 CPUs or more.  

- Authentication configuration:  
  - Change the authentication method from SSH Public Key to Password.  
  - Use the following credentials:  
    - Username: `laborer`  
    - Password: `Cyberlab123!`  

- Next steps:  
  - Click "Next: Disk."  
  - Click "Next: Networking."

<img src="https://github.com/user-attachments/assets/321d7d01-4249-4436-89a4-75c0596a0cc1" alt="Screen Shot 2025-01-07 at 21 50 28 PM" width="80%">
<img src="https://github.com/user-attachments/assets/d58bc1c8-e49c-417b-8a37-18204e87bce7" alt="Screen Shot 2025-01-07 at 21 51 25 PM" width="80%">
<img src="https://github.com/user-attachments/assets/5dba7095-44c1-4446-8c19-bd2e4c562a7d" alt="Screen Shot 2025-01-07 at 21 51 28 PM" width="80%">
<img src="https://github.com/user-attachments/assets/ab1f85cb-a742-4206-9b68-8450d2375dd0" alt="Screen Shot 2025-01-07 at 21 51 48 PM" width="80%">
<img src="https://github.com/user-attachments/assets/ddef5541-dbf2-4de3-ac4c-2c0969cae6fc" alt="Screen Shot 2025-01-07 at 21 51 58 PM" width="80%">
<img src="https://github.com/user-attachments/assets/a33bc8a7-6d7f-48b3-a65f-9a35b5e2cfc6" alt="Screen Shot 2025-01-07 at 21 52 03 PM" width="80%">
<img src="https://github.com/user-attachments/assets/ea310185-b26f-4ca7-90c0-3ba27ea3bbad" alt="Screen Shot 2025-01-07 at 21 52 29 PM" width="80%">
<img src="https://github.com/user-attachments/assets/015289e2-618b-41a7-af10-0e023102a394" alt="Screen Shot 2025-01-07 at 21 52 39 PM" width="80%">
<img src="https://github.com/user-attachments/assets/3faf4d07-f683-464d-9536-8bbaae3e3ad2" alt="Screen Shot 2025-01-07 at 21 52 42 PM" width="80%">

<li>While creating the VM, select the previously created Vnet</li>
 
<img src="https://github.com/user-attachments/assets/af2384ac-a275-44c9-b401-8b6303581a41" alt="Create a Virtual Machine" width="80%">
<img src="https://github.com/user-attachments/assets/fcc8eb89-b70a-4f0c-8fa3-ca681c5bf10c" alt="Create a Virtual Machine" width="80%">
<img src="https://github.com/user-attachments/assets/d4de0f8d-ca30-4a57-bea7-75ac0e4d697f" alt="Create a Virtual Machine" width="80%">
<img src="https://github.com/user-attachments/assets/2c6ffe3f-92aa-41d9-b5a1-1af387c1b3ed" alt="Create a Virtual Machine" width="80%">

- Click on "Go to Resource" or on the top-left corner where it says "Microsoft Azure" to return to the home page and view your resources.

<img src="https://github.com/user-attachments/assets/b7482d2c-fd98-4d23-99a2-a2c066cd0ba6" alt="Create a Virtual Machine" width="80%">
<img src="https://github.com/user-attachments/assets/9e8e9cf9-303b-4293-b336-e9f08a3bc9ce" alt="Create a Virtual Machine" width="80%">

<li>Observe Your Virtual Network within Network Watcher</li>

- Make sure both VMs are in the same Virtual Network (VNet).

<img src="https://github.com/user-attachments/assets/fa62e158-3e45-44c6-b86b-641aba5abe2e" alt="Create a Virtual Machine" width="80%">
<img src="https://github.com/user-attachments/assets/5ff474dd-3517-4e80-8604-9f7608129fae" alt="Create a Virtual Machine" width="80%">
<img src="https://github.com/user-attachments/assets/729a55aa-b75d-419b-bbec-27ddffaed405" alt="Create a Virtual Machine" width="80%">
<img src="https://github.com/user-attachments/assets/548d3046-3b91-4cff-847c-feb5715320ee" alt="Create a Virtual Machine" width="80%">

- Then, go to the Virtual Machine page.  

<img src="https://github.com/user-attachments/assets/c4c4b284-57f4-46c3-8eff-9a717a3f19d3" alt="Create a Virtual Machine" width="80%">

- You can tell your virtual machines are running.  
  - For cost savings, or if you won’t use them for a night or more than a few hours, you should stop your VMs.  

- **To Stop the VMs:**  
  - Select both VMs.  
  - Click on the "Stop" button located at the top-right, next to the "Delete" button.  
  - Wait until the status changes to **Stopped**.  

- **To Start the VMs:**  
  - When you need the VMs back online, select both VMs.  
  - Click on the "Start" button.  
  - Wait until the status changes to **Running**.  
<img src="https://github.com/user-attachments/assets/d65fe4bb-47b0-4258-97ab-d18ae0e98595" alt="Create a Virtual Machine" width="80%">
<img src="https://github.com/user-attachments/assets/7c5578a6-5c38-479a-b739-893f2c533e4f" alt="Create a Virtual Machine" width="80%">

</p>
</ol>

<h2>Observe ICMP Traffic</h2>

- If using a Mac, install **Microsoft Remote Desktop**.  
- Use Remote Desktop to connect to your Windows 10 Virtual Machine.  
- Within your Windows 10 Virtual Machine:  
  - Install **Wireshark**.  
  - Open Wireshark and start a packet capture.  
  - Filter for **ICMP traffic only**.  

- Retrieve the private IP address of the Ubuntu VM (`linux-vm`) and attempt to ping it from within the Windows 10 VM.  
  - Observe the ping requests and replies within Wireshark.  

- From the Windows 10 VM:  
  - Open Command Line or PowerShell.  
  - Attempt to ping a public website (e.g., `www.google.com`).  
  - Observe the traffic in Wireshark.  

[![Screen Shot](https://github.com/user-attachments/assets/8919c447-7e87-45fa-8598-26af70648a03)](https://youtu.be/2_FNf9q3QTc)

<h2>Configuring a Firewall (Network Security Group):</h2>

  - Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM.  
  - Open the Network Security Group (NSG) of Ubuntu VM, and disable incoming (inbound) ICMP traffic.  
  - Back in the Windows 10 VM:  
    - Observe the ICMP traffic in Wireshark and the command line Ping activity (the ping should stop working).  
  - Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using.  
  - Back in the Windows 10 VM:  
    - Observe the ICMP traffic in Wireshark and the command line Ping activity (the ping should start working again).  
  - Stop the ping activity.

<p align="center">
  <a href="https://youtu.be/of1aTFgg0kM">
    <img src="https://img.youtube.com/vi/of1aTFgg0kM/0.jpg" width="80%" />
  </a>
</p>

<h2>Observe SSH Traffic</h2>

- Log back into the `windows-vm`.  
- In Wireshark, start a packet capture.  
- Filter for SSH traffic only.  
- From your Windows 10 VM, SSH into your Ubuntu Virtual Machine using its private IP address:  
  - Open PowerShell and type: `ssh labuser@<private IP address>`  
- Type commands (username, password, etc.) into the Linux SSH connection and observe the SSH traffic in Wireshark.  
- Exit the SSH connection by typing `exit` and pressing [Enter].  

<p align="center">
  <a href="https://youtu.be/0sdMV52MVlo">
    <img src="https://img.youtube.com/vi/0sdMV52MVlo/0.jpg" width="80%" />
  </a>
</p>

<h2>Observe DHCP Traffic</h2>

- Back in Wireshark, filter for DHCP traffic only.  
- From your Windows 10 VM, issue your VM a new IP address from the command line:  
  - Open PowerShell as admin and run: `ipconfig /renew`  
- Observe the DHCP traffic appearing in Wireshark.  </p>

<p align="center">
  <a href="https://youtu.be/Q_fCYMqDARo">
    <img src="https://img.youtube.com/vi/Q_fCYMqDARo/0.jpg" width="80%" />
  </a>
</p>

<h2>Observe DNS Traffic</h2>

- Back in Wireshark, filter for DNS traffic only.  
- From your Windows 10 VM, use `nslookup` to resolve the IP addresses for `google.com` and `disney.com`:  
- Open the command line and type: `nslookup google.com` and `nslookup disney.com`.  
- Observe the DNS traffic in Wireshark.  </p>

<p align="center">
  <a href="https://youtu.be/WzQL8AFbGeU">
    <img src="https://img.youtube.com/vi/WzQL8AFbGeU/0.jpg" width="80%" />
  </a>
</p>

<h2>Observe RDP Traffic</h2>


- Back in Wireshark, filter for RDP traffic only (`tcp.port == 3389`).  
- Observe the immediate, non-stop spam of traffic.  
- **Why does RDP traffic constantly spam?**  
- RDP (Remote Desktop Protocol) constantly streams live data between two computers, so traffic is always being transmitted.  

<p align="center">
  <a href="https://youtu.be/eAUVr9meCvs">
    <img src="https://img.youtube.com/vi/eAUVr9meCvs/0.jpg" width="80%" />
  </a>
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
