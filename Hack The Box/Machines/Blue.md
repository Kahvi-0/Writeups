# Blue

![Title](https://user-images.githubusercontent.com/46513413/73159128-c82df480-40b3-11ea-96c2-5a4fef853991.png)

## Recon and enumneration

Inital port scan:

    nmap -p - -T4 -A -v 10.10.10.40
    
    -p-  scan all ports
    
    -T4 aggressive speed
    
    -A OS detection, service version scanning, script scanning and traceroute 
    
    -v verbose
    
 ## Scan results
 
![Scan 1](https://user-images.githubusercontent.com/46513413/73159143-d4b24d00-40b3-11ea-98ba-85c57bb3d912.png)
![Scan 2](https://user-images.githubusercontent.com/46513413/73159148-d5e37a00-40b3-11ea-836c-045315b90470.png)
 
 ## Enumeration notes for each discovered service 
 
 - Port 135 msrpc
 - Port 139 netbios-ssn
 - Port 445 microsoft-ds
 - Port 49152-49157 msrpc
 
 
 ## Exploitation

 Since this is a Windows 7 machine with SMB v1 enabled I am going to attempt to exploit an exploit around ms17_010 such as eternal blue.

### Using Metasploit

 Using the module "exploit/windows/smb/ms17_010_eternalblue".
 
  Check and exploit successful!
          We have root!
![SMB 1](https://user-images.githubusercontent.com/46513413/73159928-b0577000-40b5-11ea-8912-e23981f606c7.png)


### Manual exploitation
  {To do}
