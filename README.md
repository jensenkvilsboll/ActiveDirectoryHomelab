# Active Directory Homelab
**Overview**  
This project involved building and configuring a virtualized Windows domain environment to practice Active Directory administration and common IT support tasks.  

**Technologies Used**  
- Windows Server 2022
- Windows 11
- Active Directory Domain Services
- Oracle Virtualbox
  
**Lab Environment**
| System | Role |
| -------- | -------- | 
| DC01| Windows Server domain controller| 
| WIN11-01| Windows client workstation| 
| WIN11-02| Windows client workstation|   

**Skills Demonstrated**  
-Windows Server administration  
-Active Directory domain controller deployment  
-User account administration  
-Security group management  
-Virtual machine and network configuration  
-Windows file sharing and permissions  
-Network drive mapping  
-Basic IT troubleshooting  
-Technical documentation  
<br>
# Project Implementation
**1. Computer and Lab Setup**  
The focus of this section will be setting up our environment, which will include setting up the domain controller (DC01), installing services on the server, and joining workstations (WIN11-01/02) to the domain. <br>  
<img width="50%" height="50%" alt="image22" src="https://github.com/user-attachments/assets/7ba15225-81f8-4916-947e-d45292a457a7" />   
-Installed a spare HDD to provide additional storage for the lab environment.    <br>  
<img width="50%" height="50%" alt="2  partition" src="https://github.com/user-attachments/assets/e84e535d-e333-468b-b067-d83ed5c10882" />  
-Initialized and partitioned the disk using Windows Disk Management.  <br>  
<img width="50%" height="50%" alt="3  virtualization confirm" src="https://github.com/user-attachments/assets/5ec30a2d-c532-43a0-b040-3796bbdeefe2" />  
-Confirmed virtualization was enabled on current machine.  <br>  
<img width="50%" height="50%" alt="4 windows server install" src="https://github.com/user-attachments/assets/38587eab-8e19-4a86-bbf4-5c514e4744d6" />  
-Add a new machine and install Windows Server 2022.  <br>  
<img width="50%" height="50%" alt="5 win11-01" src="https://github.com/user-attachments/assets/e830638f-7174-4079-97eb-e9c6bf977f89" /><img width="50%" height="50%" alt="6 win11-02" src="https://github.com/user-attachments/assets/794215f7-5097-488d-bd17-33e20bbc3184" />  
-Add two more machines and install Windows 11 Pro on each of them.  <br>  
<img width="50%" height="50%" alt="7 HostNatConf" src="https://github.com/user-attachments/assets/666df9f8-bae0-4a08-bf8d-d1da2c087a01" />  
-On each machine, go to Settings> Network and set adapter 1 to Host-only Adapter, and adapter 2 to NAT. This allows the VMs to communicate with eachother, while keeping them isolated from home network, and to have an internet connection.  <br>  
<img width="50%" height="50%" alt="image" src="https://github.com/user-attachments/assets/ac508c3c-ba29-40ce-aad0-fe6bd0c1407c" />  
-Go to File> Tools> Network, and disable DHCP server. This will allow DC01 to be used as DHCP server.  <br>  
<img width="50%" height="50%" alt="image" src="https://github.com/user-attachments/assets/ee922a7e-a44c-44b6-91b5-ca121f4b85d6" />  
-On DC01, it will be given a static IP address of 192.168.56.2/24 and since we have a single domain controller in this lab, the DNS will be set itself, 127.0.0.1.  <br>  
<img width="50%" height="50%" alt="8 ADins" src="https://github.com/user-attachments/assets/7efac67f-638f-4f3d-9190-48c75b38683f" /><img width="50%" height="50%" alt="image" src="https://github.com/user-attachments/assets/35444f5a-7760-47d3-ba07-4655b9c97be7" />  
-Install Active Directory Domain Services, DHCP Server, and DNS server on DC01 through Server Manager.  <br>  
<img width="50%" height="50%" alt="13 Promoting to domain controller" src="https://github.com/user-attachments/assets/7c9825b3-67d1-418a-97b8-ed91e163b49b" />  
-Promoted DC01 to a domain controller for the HOMELAB.local Active Directory domain.  <br>  
-<img width="48%" height="48%" alt="14 DCHP SCOPE 1" src="https://github.com/user-attachments/assets/5fe40674-5e28-4b04-8359-2bf9c2da2877" /><img width="50%" height="50%" alt="14 DCHP SCOPE 2" src="https://github.com/user-attachments/assets/b4b7e654-0dce-43e5-9d69-12f223dd9ef7" />    <img width="50%" height="50%" alt="14 DCHP SCOPE 4" src="https://github.com/user-attachments/assets/5698dc3e-565a-4d35-b174-c73dda387647" /><img width="50%" height="50%" alt="14 DCHP SCOPE 5" src="https://github.com/user-attachments/assets/5d680501-acde-40e9-af0b-37f07e1085fd" />    
-In Server Manager> Tools> DHCP> dc01.homelab.local, right-click on IPv4 and selected new scope. Created and activated an IPv4 scope for the 192.168.56.0/24 subnet, configured an address pool from 192.168.56.50 to 192.168.56.100, and set DC01 (192.168.56.2) as the DNS server.  <br>  
<img width="50%" height="50%" alt="15 win11-01 dns" src="https://github.com/user-attachments/assets/990fc479-f1ca-4117-a987-123305482beb" /><img width="50%" height="50%" alt="16  win11-01 ipconfig" src="https://github.com/user-attachments/assets/d129022e-5c56-4363-bf20-d0a21d156e40" />  
-On both Workstations, Control Panel> Network and Internet> Network and Sharing Center> Change adapter settings> right-click Ethernet> Properties> IPv4 Properties and set IP address to obtain automatically via DHCP and point the DNS server address to DC01 (192.168.56.2).  <br>  
<img width="50%" height="50%" alt="17 domain join" src="https://github.com/user-attachments/assets/c0beb4a6-9198-4c22-adce-6f2e20ab21b6" /><img width="50%" height="50%" alt="18  confirm" src="https://github.com/user-attachments/assets/e2c12373-7086-4f2f-a2a9-0d1ce17bcd26" />    
-On both Workstations, Settings> System> About> Domain or Workgroup> Change and make it a member of the domain HOMELAB.local.  <br>  
**2. Users, Groups, and Policies Setup**  
The focus of this section will be creating users, organizational units, and security groups. We will also be adding users to the security groups and configuring Group Policy Objects. <br>  

<img width="50%" height="50%" alt="20  security groups" src="https://github.com/user-attachments/assets/b7b9f137-7123-4182-a405-663bce21063e" /><img width="50%" height="50%" alt="19  users" src="https://github.com/user-attachments/assets/f9a3ad00-de23-41a0-99ab-c73fcef43bb1" />
<img width="50%" height="50%" alt="21  workstations" src="https://github.com/user-attachments/assets/2d1b9ef3-7f7e-4bd9-849d-5cbc7790805c" />  <br>
-To create organizational units (OU's), right click on the domain, select New> Organizational Unit, and create an OU for the accounts, security groups and workstations.  
-In the Groups OU, right click Groups> New> Group, and create the groups needed.  
-In the Accounts OU, right click Accounts> New> User, and add the users first name, last name, and their user logon name.  
-For workstations added to your domain, it is best practice to move them into their own OU, since the Computers folder in AD is a container, not an OU. This allows you to implement GPOs. When the workstation joins your domain in Computers, right click the workstation and move it to the Workstation OU. You can also use the redircmp command in an elevated Command Prompt to automatically redirect new workstations added to the OU, instead of the Computers container.  <br>  
<img width="50%" height="50%" alt="22 new gpo" src="https://github.com/user-attachments/assets/d799f863-79c3-4853-bef6-40886d911450" />  <br>
-To create a new GPO, in server manager, go to Tools> Group Policy Management. Then, under the domain, right click Group Policy Objects, select New, and name the new GPO.  <br>  
<img width="50%" height="50%" alt="23 link gpo" src="https://github.com/user-attachments/assets/3aedfb6c-b846-4fee-81f0-9891fa02936f" />  
-Then right click workstations> New> Link an Existing GPO...> add the newly created GPO.  <br>  
**Group Policy Configuration**

<img width="50%" height="50%" alt="24 prevent background" src="https://github.com/user-attachments/assets/6eba2383-1d2f-4486-985a-af5d31677c01" />  <br>
-This policy will prevent users from changing their desktop background demonstrating user restriction. To edit this policy, edit Workstation Security Policy> User Configuration> Policies> Administrative Templates> Control Panel> Personalization> Prevent changing desktop background.  <br>  
<img width="50%" height="50%" alt="25 prevent access to control panel" src="https://github.com/user-attachments/assets/6c355518-fbbe-4653-b890-83017fa305db" />  <br>
-This policy will prevent access to Control Panel and PC settings demonstrating restricting user access to system settings. To edit this policy, edit Workstation Security Policy> User Configuration> Policies> Administrative Templates> Control Panel> Prohibit access to Control Panel and PC settings.  <br>  
<img width="50%" height="50%" alt="26 lock inactive computers" src="https://github.com/user-attachments/assets/195d7f2c-20b4-4906-b82c-c274268dc4e1" />  <br>
-This policy will automatically lock inactive computers after 600 seconds demonstration basic workstation security. To edit this policy, edit Workstation Security Policy> Computer Configuration> Policies> Windows Settings> Security Settings> Local Policies> Security Options> Interactive logon: Machine inactivity limit.  <br>  
<img width="50%" height="50%" alt="27 firewall" src="https://github.com/user-attachments/assets/9b6f8e7a-4176-43ec-b84c-e8caa423b578" />  <br>
-This policy will enable the firewall for domain, public, and private profiles demonstrating endpoint security. To edit this policy, edit Workstation Security Policy> Computer Configuration> Policies> Windows Settings> Security Settings> Windows Defender Firewall with Advanced Security.  <br>  
<img width="50%" height="50%" alt="28 password requirements" src="https://github.com/user-attachments/assets/9e7386cf-21e0-4df2-8173-1ded87f8d7b2" />  <br>
-This policy will configure domain password requirements demonstrating domain account security. To edit this policy, edit Default Domain Policy> Computer Configuration> Policies> Windows Settings> Security Settings> Account Policy> Password Policy.  <br>  
<img width="50%" height="50%" alt="29 windows update" src="https://github.com/user-attachments/assets/4f3e139b-ee37-4038-95b8-168fa00d13e2" />  <br>
-This policy will configure automatic Windows Update behavior demonstrating patch management. To edit this policy, edit Workstation Security Policy> Computer Configuration> Policies> Administrative Templates> Windows Components> Windows Update> Configure Automatic Updates.  <br>  
<img width="50%" height="50%" alt="30usb" src="https://github.com/user-attachments/assets/5d5cabf5-7308-4b81-b160-f0097af7d981" />  <br>
-This policy will restrict USB storage devices demonstration data protection. To edit this policy, edit Workstation Security Policy> Computer Configuration> Policies> Administrative Templates> System> Removable Storage Access> All Removable Storage classes: Deny all access.  <br>  
<img width="50%" height="50%" alt="31 gpupdate" src="https://github.com/user-attachments/assets/499af4b3-a134-43b2-892d-277ab4e60928" />  <br>
-After configuring the GPOs, run gpupdate and gpresult /r, to verify changes.  <br>  
**3. Troubleshooting and Verification**  






















