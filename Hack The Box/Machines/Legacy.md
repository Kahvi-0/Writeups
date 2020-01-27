# Legacy

![Title](https://user-images.githubusercontent.com/46513413/73158213-2efdde80-40b1-11ea-8777-d2271ac1975d.png)


## Recon and enumneration

Inital port scan:

    nmap -p - -T4 -A -v 10.10.10.40
    
    -p-  scan all ports
    
    -T4 aggressive speed
    
    -A OS detection, service version scanning, script scanning and traceroute 
    
    -v verbose

## Scan results
    
![Scan](https://user-images.githubusercontent.com/46513413/73158317-7be1b500-40b1-11ea-9e53-38b9c7a48871.png)
![Sccan 2](https://user-images.githubusercontent.com/46513413/73158319-7e440f00-40b1-11ea-8498-91910e2522a3.png)

 
 ## Enumeration notes for each discovered service 
 
  - Port 139
  - Port 445
    SMB v1 and v2
 
 ![Smb enum](https://user-images.githubusercontent.com/46513413/73158436-cbc07c00-40b1-11ea-997f-f247ea21bbd0.png)

 
 ## Exploitation
  
   Since this is a Windows XP machine with SMB v1 enabled I am going to attempt to exploit eternal blue.
  

### Using Metasploit

 I am going to try to use the metaploit module "exploit/windows/smb/ms17_010_psexec"
 
![exploit 2](https://user-images.githubusercontent.com/46513413/73158598-4b4e4b00-40b2-11ea-9883-555a82dbfb60.png)

![Exploit 3](https://user-images.githubusercontent.com/46513413/73158632-68831980-40b2-11ea-9814-c3a185aa98ff.png)

![Getsystem](https://user-images.githubusercontent.com/46513413/73158682-92d4d700-40b2-11ea-8e06-bd7133e3a6bc.png)

 
### Manual exploitation

  {To add}

 
 Now I am able to go grab the John and Administrator user flags. 
 
![John 2](https://user-images.githubusercontent.com/46513413/73158806-f3641400-40b2-11ea-8a4d-875ee8f8076e.png)
![Admin flag](https://user-images.githubusercontent.com/46513413/73158809-f4954100-40b2-11ea-8853-73b51ab188b3.png)


# Final notes
 
 Please patch/upgrade OS/Services :) 
