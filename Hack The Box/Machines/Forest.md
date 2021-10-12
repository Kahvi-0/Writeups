# Forest 

## Recon and enumneration

Inital port scan using the nmap TCP scan from https://github.com/Kahvi-0/Projects/blob/master/netScan/netScan.sh

    nmap -p - -T4 -A -v <IP>
    
    -Pn assume host is up
    -p-  scan all ports 
    -T4 aggressive speed 
    -A OS detection, service version scanning, script scanning and traceroute  
    -v verbose
    
    
## Scan results
![portscan1](https://user-images.githubusercontent.com/46513413/136888440-d26aecfc-df93-4f99-a563-56b2dcc0aac9.PNG)
![portscan2](https://user-images.githubusercontent.com/46513413/136888451-076e7daa-b239-4c41-a310-ec50ad48d699.PNG)

 
## Enumeration notes for each discovered service 
 
 
## Exploitation

### Using <tool assisted>
 
 
### Manual exploitation


# Final notes and lessons learned
 
 This box is the first challenge that required me to use BloodHound and allowed me the operatunity to look more into automated AD enumeration tools. 
 During and after I researched other peoples methods of using BloodHound and other tools such as ACLPwn that can be used when enumerating future AD devices.
 
 

