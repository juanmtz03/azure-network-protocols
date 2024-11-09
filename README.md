<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 
- Ubuntu Server 

<h2>Setting Up Sample File Shares with Various Permissions</h2>

First, log into DC-1 as a domain admin and Client-1 as a regular user to set up file shares with varying permissions. On DC-1, create four folders named “read-access,” “write-access,” “no-access,” and “accounting” on the C:\ drive. Assign permissions for each: “Domain Users” have “Read” access to “read-access,” “Read/Write” to “write-access,” and no access to “no-access” (restricted to “Domain Admins” only). Test these permissions on Client-1 by attempting to access each folder. Then, create an “ACCOUNTANTS” security group in Active Directory, set the “accounting” folder to “Read/Write” for this group, and verify that a regular user cannot access it. After adding this user to the “ACCOUNTANTS” group, log in again to confirm they can now access the “accounting” folder as expected.

<h2>Create some sample file shares with various permissions</h2>

- **Set Folder Permissions**
  - **Folder:** `read-access`  
    **Group:** `Domain Users`  
    **Permission:** `Read`
    
  - **Folder:** `write-access`  
    **Group:** `Domain Users`  
    **Permission:** `Read/Write`
    
  - **Folder:** `no-access`  
    **Group:** `Domain Admins`  
    **Permission:** `Read/Write`
    
  - Skip setting permissions for `accounting` for now.

<div align="center" style="display: grid; grid-template-columns: 4fr 1fr; gap: 5px; width: 80%; max-width: 400px;">
<img src="https://github.com/user-attachments/assets/c35f7742-ac3a-49cb-a296-ea8ce8210bfc" alt="image" style="width: 50%; height: auto;">
<img src="https://github.com/user-attachments/assets/afc6c96d-7279-4e90-aaca-7a06d54ea936" alt="image" style="width: 50%; height: auto;">
<img src="https://github.com/user-attachments/assets/af35c269-d997-4bfe-b017-3a1d4d83c7bc" alt="image" style="width: 50%; height: auto;">
<img src="https://github.com/user-attachments/assets/42cc7397-44f9-4771-837e-9725462c0633" alt="image" style="width: 50%; height: auto;">
</div> 
<br />

<h2>Attempt to access file shares as a normal user</h2>

- **Test File Share Access**
  - On `Client-1`, login as a normal user (`mydomain\<bab.cif>`).
  - Navigate to the shared folder using `\\dc-1`.
  - Attempt to access the folders. Check which folders you can view and which ones allow file creation.

<div align="center" style="display: grid; grid-template-columns: 4fr 1fr; gap: 5px; width: 80%; max-width: 400px;">
<img src="https://github.com/user-attachments/assets/6e7feb6a-b183-4dde-ba04-4ea763c4b25b" alt="image" style="width: 50%; height: auto;">
<img src="https://github.com/user-attachments/assets/1dbcc794-7f2a-4b19-8eda-1ce5bb1fa903" alt="image" style="width: 50%; height: auto;">
</div> 
<br />

<h2>Create an “ACCOUNTANTS” Security Group, assign permissions, an test access</h2>

- **Set Up ACCOUNTANTS Security Group and Assign Permissions**
  - On `DC-1`, in Active Directory, create a new security group called `ACCOUNTANTS`.
  - On the `accounting` folder, set the following permissions:
    - **Folder:** `accounting`  
      **Group:** `ACCOUNTANTS`  
      **Permission:** `Read/Write`
  - Log in to `Client-1` as `<bab.cif>` and try to access the `accounting` folder. Access should be denied.

- **Add User to ACCOUNTANTS Group and Re-Test Access**
  - On `DC-1`, add `<bab.cif>` to the `ACCOUNTANTS` security group.
  - Sign back into `Client-1` as `<bab.cif>` and try to access the `accounting` folder at `\\DC-1\`. Access should now be granted.

<div align="center" style="display: grid; grid-template-columns: 4fr 1fr; gap: 5px; width: 80%; max-width: 400px;">
<img src="https://github.com/user-attachments/assets/8b579ab4-89fc-4fee-8e24-8fb4478cd913" alt="image" style="width: 50%; height: auto;">
<img src="https://github.com/user-attachments/assets/e776f6d3-71b6-4257-8d92-f49c444fa39d" alt="image" style="width: 50%; height: auto;">
<img src="https://github.com/user-attachments/assets/eaf4214d-cfe3-44e9-b01a-7c5e49301e89" alt="image" style="width: 50%; height: auto;">
<img src="https://github.com/user-attachments/assets/cd923777-ac26-47dd-b189-9f8e79c4ee9d" alt="image" style="width: 50%; height: auto;">
<img src="https://github.com/user-attachments/assets/9535acb5-3bd9-42c7-a8a9-90bc26f0ea89" alt="image" style="width: 50%; height: auto;">
<img src="https://github.com/user-attachments/assets/66ab67fb-efc6-4393-88a7-d8fb72bdbd16" alt="image" style="width: 50%; height: auto;">
<img src="https://github.com/user-attachments/assets/5d5cf971-d9d9-4326-b14e-9c9fa16ab2ff" alt="image" style="width: 50%; height: auto;">
<img src="https://github.com/user-attachments/assets/9c0c0b38-0fd3-4a2a-9c07-78edc2212031" alt="image" style="width: 50%; height: auto;">
  
</div> 
<br />


