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
- Setting Up Active Directory Domain Services (AD DS)
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
## Verifying that DNS is working

1. To verify that DNS is working, all I had to do was examine the results of me **pinging google.com** from inside of the VM. Because I received replies from google.com with an IPv6 address, I can conclude that DNS works. 

![ActiveDirectoryDNS](https://github.com/user-attachments/assets/98910f9d-cc2a-4655-bd2c-ac6eecdffa40)
(Output of the command *ping google.com*)

---
## Setting Up Active Directory Domain Services (AD DS)

1. I first selected the **AD DS** tab on the left of **Server Manager.** I then clicked **Promote this server to a domain,** thus opening the configuration wizard.
2. Next, at the **Deployment Configuration** tab, I selected **Add a new forest** and made the root domain name **Electricx.local**
![ActiveDirectory9](https://github.com/user-attachments/assets/5dfa2db5-7438-46e4-ac5f-c5fbc8d1c4fe)
   (The AD DS Configuration Wizard)

3. Then, at the **Domain Controller Options** tab, I set the **Forest functional level** and the **Domain functional level** to Windows Server 2016 and checked the **Domain Name System (DNS) Server** box. I then typed in the **Directory Services Restore Mode (DSRM) password.**
![ActiveDirectory10](https://github.com/user-attachments/assets/c9b51153-1672-40a2-b897-9ec3c94c5b0c)
   (The Domain Controller Options tab)

4. I then proceeded to the **Prerequisites Check** tab and waited for the prerequisite checks to pass successfully and then clicked **Install.**
![ActiveDirectory11](https://github.com/user-attachments/assets/02d946ad-313b-455c-8131-f11d546e5a19)
   (Installing AD DS)

5. My system then automatically restarted, and upon re-entering my password and going back to the AD DS tab, I saw that AD DS has been installed for my domain.
![ActiveDirectory12](https://github.com/user-attachments/assets/b7bd2225-4cf0-4252-8683-69586e27cae5)
   (My username being changed to ELECTRICX (my domain)\Administrator (my previous username))
![ActiveDirectory13](https://github.com/user-attachments/assets/76edb267-1aa4-4b29-aa0b-d80f1061240a)
   (AD DS all setup)
