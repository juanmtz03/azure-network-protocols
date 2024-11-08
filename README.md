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

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

- **Create File Shares on DC-1**
  - Log into `DC-1` as the domain admin account `mydomain.com\jane_admin`.
  - On the `C:\` drive, create the folders: `read-access`, `write-access`, `no-access`, and `accounting`.

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

<br />


<h2>Attempt to access file shares as a normal user</h2>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

- **Test File Share Access**
  - On `Client-1`, login as a normal user (`mydomain\<someuser>`).
  - Navigate to the shared folder using `\\dc-1`.
  - Attempt to access the folders. Check which folders you can view and which ones allow file creation.
<br />

<h2>Create an “ACCOUNTANTS” Security Group, assign permissions, an test access</h2>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

- **Set Up ACCOUNTANTS Security Group and Assign Permissions**
  - On `DC-1`, in Active Directory, create a new security group called `ACCOUNTANTS`.
  - On the `accounting` folder, set the following permissions:
    - **Folder:** `accounting`  
      **Group:** `ACCOUNTANTS`  
      **Permission:** `Read/Write`
  - Log in to `Client-1` as `<someuser>` and try to access the `accounting` folder. Access should be denied.

- **Add User to ACCOUNTANTS Group and Re-Test Access**
  - On `DC-1`, add `<someuser>` to the `ACCOUNTANTS` security group.
  - Sign back into `Client-1` as `<someuser>` and try to access the `accounting` folder at `\\DC-1\`. Access should now be granted.

<br />


