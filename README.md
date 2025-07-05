# Active Directory (WIP)

## Objective

To install and navigate Active Directory to gain hands-on experience with its core functions.

# Why Active Directory?

**Active Directory (AD)** is a directory service from Microsoft that is used to manage users, groups, computers, policies, permissions, and resources within a Windows-based network. It functions as the brain, dictating who can access what, when, and how. It is installed on a **Domain Controller,** which is what stores and manages the information above for the entire network (or domain). As an IT professional, it's important to understand how to navigate and use Active Directory because it's used daily to **reset passwords, create, disable, or delete user accounts, join new computers to the domain, push group policy updates (e.g., auto-lock screens after 5 min), grant or restrict access to shared folders and systems, audit login attempts and track suspicious activity, organize users by department, location, or security level, apply software installs or updates remotely, delegate control to junior IT or helpdesk staff safely, and backup and restore AD objects.**

With this project, my goal to gain hands-on experience with all 10 of the above to assist me with a future IT job/internship. 
 
### Skills Learned

- Installing Windows Server 2022
- Installing Server Manager
- Setting a Static IP Adress
- Verifying that DNS is working
- Testing Domain Join 
- Setting Up Active Directory
- Create, Disable, and Delete User Accounts
- Create Security Groups and Add Users
- Organizing with Organizational Units (OUs)
- Using Group Policy Objects (GPO)
- Setting Permissions on Shared Folders
- Resetting Passwords for Users
- Joining New Computers to the Domain
- Enabling Auditing for Login Attempts
  

### Tools Used

- VMware
- Windows Server 2022
- Windows Server Manager
- Powershell



---
## Steps

## Installing Windows Server 2022

1. I first navigated to Microsoft's website after searching "Windows Server 2022 download." I filled out the short questionaire and then downloaded the 64-bit .iso file. 
![ActiveDirectory3](https://github.com/user-attachments/assets/3fee2084-ecb9-4bc7-ac9f-234eb5b24577)
(The short questionaire form)


![ActiveDirectory4](https://github.com/user-attachments/assets/0ca79d68-e899-41af-9531-cadbf578dc4d)
(Downloading the .iso file)

2. I then installed the VM to VMware the same way as the Windows 10 VM, but I also ensured to go into the VM's settings and select the .iso file in **CD/DVD (SATA)**
![ActiveDirectory5](https://github.com/user-attachments/assets/f507d16e-a587-406c-8ca1-528aff261948)
   (Configuring the VM)

3. While following the setup, I made the username Administrator and set a password. After completing a few more prompts and waiting for the system to finish its download, my server was ready to go.
![ActiveDirectory6](https://github.com/user-attachments/assets/7e76fcbc-e652-4c01-a47d-814fb3a327e5)
   (Making the Domain Controller account)

---
## Installing Server Manager

I originally thought that Active Directory was setup on a regular PC, but that was wrong. As such, the screenshots below show me downloading Server Manager on my Windows 10 VM. Please keep in mind that I followed these same steps but with my Windows Server 2022. 

1. To install Server Manager, I first opened **Settings** and then **Optional Features**
2. Then, I clicked **Add a Feature** and installed:
   - RSAT: Server Manager
   - RSAT: Active Director Domain Services and Lightweight Directory Services Tools
   - RSAT: Active Directory Certificate Services Tools
   - RSAT: Group Policy Management Tools

![ActiveDirectory1](https://github.com/user-attachments/assets/4fb07486-d6ff-402f-80c6-633f4c8c2e20)
    (Me installing Server Manager)

---
## Setting a Static IP Address

1. First, to make sure that my VM would run on a static IP address, I went into VMware and then selected **VM,** **Settings,** and then **Network Adapter.** I then set my network connection to **Bridged: Connect directly to the physical network.**
2. Because the bridged connection was not working, I had to troubleshoot it by going into **Edit** and then **Virtual Network Editor** to configure the **VMnet0** connection. After setting it to the proper Ethernet adapter (since my VM is connected to the internet via my host PC's ethernet cable), my bridged connection issues were resolved.
3. After resolving the network issues, I opened **Powershell** on my host machine and used the *ipconfig /all* command, taking note of the IPv4 address, Subnet Mask, Default Gateway, and DNS Server(s) under the **Ethernet adapter Ethernet:** section.
4. Next, I opened my Windows Server and went to **Server Manager,** then **Local Server.** I then clicked on **IPv4 address assigned by DHCP** and selected **Properties** after right-clicking my Ethernet adapter. I then selected **Internet Protocol Version 4 (TCP/IPv4)** and then right-clicked to select **Properties.** Then I clicked **Use the following IP address:** and **Use the following DNS server addresses:** and set these five fields:

- IP address
- Subnet Mask
- Default Gateway
- Preferred DNS Server
- Alternate DNS Server

I then clicked **Apply** and **OK.**

5. Finally, I tested the Windows Server by opening Powershell and running the *ipconfig* command to ensure that what I set in the previous step matched the output of the command. I then pinged my router, 8.8.8.8, and google.com to ensure the connection existed. 


---
## Skill 4


