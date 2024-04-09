Active Directory Infrastructure Simulated Environment Project

Purpose: A virtualized environment that simulates a small business network.

Tools: Oracle Virtual Box

OSs: Windows Server 2016, Windows 10

In this lab I’ve noted important information involved in setting up and operating a Microsoft AD environment. I installed Server 2016, activated AD domain services. Then I installed Windows 10, installed RSAT tools (Remote Server Administrator Tools) and joined the VM to the domain.

**Step 1: Virtualization and Domain Setup**

1.  Download Server 2016 from Microsoft’s Evaluation Center
2.  Select Windows Server 2016 Standard Evaluation (Desktop Experience) for GUI support. Core editions do not include GUI support.
3.  Minimum hardware requirements for Server 2016 Desktop Experience: 2 GB RAM. 32 GB storage space.
4.  Hostname: CorpDC
5.  Create Active Directory Domain Services
    1.  Server Manager \> Manage \> Add Roles and Features \> Role-based or feature-based installation.
    2.  Select “Active Directory Domain Services” from the Roles checkboxes.
    3.  Install Features
    4.  Click “Promote this Server to a Domain”.
    5.  Root domain name: kreed.com
    6.  Admin account: vboxuser. Name: Kurt Reed

**Step 2: AD Management & User Management**

1.  Go to Active Directory Users and Computers. Make the admin user account a member of: Domain Admins, Enterprise Admins, Group Policy Creators and Schema Admins security groups.
    1.  Restart the machine to apply policies.
2.  Go to Active Directory Administrative Center. Enable Recycle Bin. Refresh the Active Directory Administrative Center.
    1.  Once the change has been replicated, the deleted objects folder will appear under the kreed domain.
3.  Create a help desk account with admin rights.
    1.  Right click on Administrator account \> copy.
    2.  First name: helpdesk. Logon name: helpdesk

![A screenshot of a computer Description automatically generated](media/64efa4bc89c9f3570f16a957acfd0b12.png)

**Step 3: Adding the first computer to the domain.**

1.  Installing Windows 10 machine in VirtualBox
    1.  Use Microsoft Media Creation Tool
    2.  Select “Create installation media”
2.  VirtualBox Windows 10 machine setup
    1.  Name: Windows 10 Lab
    2.  Username: vboxuser01. Password: 3898
    3.  Minimum hardware requirements for Windows 10 (x64): 2GB RAM, 1 CPU core, 32 GB storage space.
    4.  Select Windows 10 Pro so we can add the computer to a domain.
3.  Create static IP for Windows Server.
    1.  The internet won’t work but will allow the lab environment to function.
    2.  IP settings

| IP            | 10.1.10.2 |
|---------------|-----------|
| Subnet mask   | 255.0.0.0 |
| Gateway       | 10.1.10.1 |
| DNS           | 10.1.10.2 |
| DNS alternate | 10.1.10.1 |

1.  Network and Sharing Center \> Change Adapter Settings \> Properties \> Internet Protocol Version 4 \> Enter network settings
    1.  Select Virtual Box Devices tab \> Network Settings \> Change “Attached to:” to “Host-only Adapter”
2.  Windows 10 machine setup
    1.  Create local account
    2.  Enable Administrator account
        1.  Local Users and Groups \> select properties for the admin account \> uncheck “Account is disabled”
        2.  Change password
    3.  Login as Administrator
        1.  Delete “User” account
    4.  Go to Optional Features \> Add an optional feature \> Select the options below \> Install
        1.  RSAT: Active Directory Certificate Services Tools
        2.  RSAT: Domain Services
        3.  RSAT: DHCP Server Tools
        4.  RSAT: DNS Server Tools
        5.  RSAT: Group Policy Management Tools
        6.  RSAT: Remote Desktop Services Tools
        7.  RSAT: Server Manager
    5.  Active Directory tools are now downloaded for Windows 10. This will allow the help desk account we created to use Active Directory tools without needed access to the Domain Controller.

        ![A screenshot of a computer Description automatically generated](media/2cde3ff8df1ad50889294771863a03e7.png)

    6.  Restart the machine.
3.  Adding the Windows 10 computer to the domain and setup
    1.  Change name of computer to “Desktop1”
        1.  Settings \> About \> Change name
    2.  Download Google Chrome and TeamViewer on Windows 10 Lab
    3.  Change IPv4 settings of Ethernet Adapter
        1.  ![A screenshot of a computer Description automatically generated](media/20ff16e43fac02ed167b76f2461460c9.png)
    4.  Select VirtualBox Devices tab \> Network Settings \> Select “Host-adapter only”
    5.  On Windows 10 machine go to About in Settings \> Advanced system settings \> Computer Name \> Change \> Type in domain “kreed.com”
        1.  Enter the credentials for the admin account on the domain controller. Username: vboxuser
    6.  The Windows 10 machine should now be a member of the kreed.com domain. Go to Computers in Active Directory Users and Computers on the Windows Server machine to verify. DESKTOP1 should be listed.
    7.  Sign in to the Windows 10 machine with the help desk account
        1.  Username: helpdesk

**Step 4: Setting up Desktop 2**

1.  Set up Desktop 2 in VirtualBox
    1.  Minimum RAM for Windows 10 (64-bit) is 2GB. 8GB recommended. Minimum disk space of 32 GB.
    2.  Select Windows 10 Pro
