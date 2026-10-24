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
<br>
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
-On DC01, it will be given a static IP address of 192.168.56.2/24 and preferred DNS will set to 127.0.0.1, meaning that it will be pointing to its own DNS service.  <br>  
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
