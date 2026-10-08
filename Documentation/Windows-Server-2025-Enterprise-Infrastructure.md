Enterprise Windows Server Infrastructure

1. Project Overview

This project demonstrates the implementation and administration of an Highly Available Enterprise Windows Server 2025 domain environment 

The environment includes Active Directory Domain Services, Organizational Units, users and groups, Group Policy, DHCP, DHCP Failover, DNS, IIS, file sharing, network drives, printer management, Active Directory Recycle Bin, Hyper-V, Hyper-V Replica, domain client integration, and scheduled server backup.

2. Lab Requirements

#	Requirement
1	Create FINAL.LOCAL domain on PDC
2	Create department OUs
3	Create users and department groups
4	Configure password policy
5	Configure account lockout
6	Enable Remote Desktop through GPO
7	Configure Remote Assistance
8	Restrict external storage, Task Manager and Control Panel
9	Configure DHCP
10	Configure DHCP Failover and ADC
11	Install IIS
12	Configure DNS load balancing
13	Configure shared folders
14	Configure mapped drives
15	Configure public folder and quota
16	Configure printer restrictions
17	Enable AD Recycle Bin
18	Configure Hyper-V and Hyper-V Replica
19	Join client to domain
20	Configure daily server backup


3. Lab Infrastructure
3.1 Servers
Server	Role	IP
PDC	Primary Domain Controller	192.168.1.2
ADC	Additional Domain Controller / DHCP Failover	192.168.1.3
Core VM	Windows Server Core VM	DHCP Assigned
Client	Domain Client	DHCP Assigned


4. Active Directory Domain Services
4.1 Domain Creation

Requirement

Domain Name: FINAL.LOCAL
Server Name: PDC
IP Address: 192.168.1.2/24
Gateway: 192.168.1.1
Implementation

Screenshot:
01-PDC-Domain-Configuration.png

Description:

The PDC server was configured as the primary domain controller for the FINAL.LOCAL Active Directory domain.

5. Organizational Units

FINAL.LOCAL
│
├── HR
├── Sales
├── Dev
└── IT


Screenshot
02-Department-OUs-and-Groups.png

6. Users and Groups

Department
   ├── Users
   └── Department Group

Screenshots
03-Users-and-Group-Membership.png

7. Group Policy – Password Policy

Password expiration: 60 days
Minimum password length: 6
Complexity: Enabled
Remember last 3 passwords

Screenshot
04-Password-Policy.png

8. Account Lockout Policy

4 failed attempts
Lockout duration: 1 hour

Screenshot
05-Account-Lockout-Policy.png

9. Remote Desktop

Enable RDP for all domain computers using Group Policy.

Screenshot
06-Remote-Desktop-GPO.png

10. Remote Assistance

Enable Remote Assistance
IT Group as helpers

Screenshot
07-Remote-Assistance-GPO.png

11. Security Restrictions

External storage
Task Manager
Control Panel

Screenshot
08-External-Storage-GPO.png
09-Task-Manager-GPO.png
10-Control-Panel-GPO.png

12. DHCP
Scope
Start: 192.168.1.40
End:   192.168.1.230
Subnet: /24
Exclusion
192.168.1.80 – 192.168.1.85
Lease
10 Days

Screenshots
11-DHCP-Scope.png
12-DHCP-Exclusion.png
13-DHCP-Lease-Duration.png
14-DHCP-Router-Gateway.png

13. ADC(core) 

ADC:

Hostname: ADC
IP: 192.168.1.3
Role: Additional Domain Controller

Screenshots
15-ADC-IP-Configuration.png
16-ADC-Joining-Domain.png
17-Win-Core-as-ADC.png
18-Installing-DHCP-on-Core-ADC.png

14. DHCP Failover

Screenshots
19-DHCP-Failover.png
20-DHCP-Failover2.png

14. IIS Web Server

PDC
ADC

Default IIS page.

Screenshots
21-IIS-on-PDC.png
22-Installing-WebServer-on-Core-ADC.png
23-IIS-on-ADC.png

15. DNS Load Balancing

DNS record:

www.final.local

192.168.1.2
192.168.1.3

Screenshots
24-DNS-Records-Load-Balancing.png

16. Shared Folder – Dev & HR

Dev + HR

Create
Edit
Cannot Delete


Porhibit:
1-Audio
2-Video
3-Executable files

Screenshots
25-Shared-Folder-HR-Permissions.png
26-Security-Folder-HR-Permissions.png
27-Shared-Folder-Dev-Permissions.png
28-Security-Folder-HR-Permissions.png
29-Dev-File-Screening.png
30-HR-File-Screening.png

17. Mapped Network Drive

Screenshot
31-Department-Mapped-Drive.png

18. Public Folder & Quota

Domain Users:

Can edit
Maximum quota: 2 GB

Screenshots
32-Public-Folder-Permissions.png
33-Public-Folder-Quota.png

19. Printer

All domain users
Black & White printing
Printing time: 09:00 AM – 04:00 PM

Screenshot
34-Printer-Color.png
35-Printer-Schedule.png

20. Active Directory Recycle Bin

Enable AD Recycle Bin.

Screenshot
36-AD-Recycle-Bin.png

21. Hyper-V

Install Hyper-V on:

PDC
ADC

Create a Core VM on PDC.

Screenshots
37-Core-VM.png

22. Hyper-V Replica

Configure replication:

PDC
 │
 │ Hyper-V Replica
 ▼
ADC

Screenshots
38-Hyper-V-Replica-Configuration.png
39-Replication-in-ADC.png

23. Client Domain Join

Join client machine to:

FINAL.LOCAL

Screenshot
40-Client-Domain-Join.png
41-Client-Join-in-AD-Computers.png

24. Windows Server Backup

Backup Type: Full Server
Frequency: Daily
Time: 11:00 PM
Destination: ADC

Screenshots
42-Backup-Configuration.png
43-Backup-Schedule.png
44-Backup-Destination.png
45-Backup-Status.png

25. Testing & Verification

Component	Test	Expected Result	Status
AD	Domain login	Successful	✅
DNS	www.final.local	Resolves to configured IPs	✅
DHCP	Client request	Gets valid IP	✅
RDP	Remote connection	Successful	✅
Shared Folder	Dev/HR access	According to permissions	✅
IIS	Open web page	Default IIS page	✅
Hyper-V Replica	Replication health	Healthy	✅
Backup	Scheduled backup	Successful	✅