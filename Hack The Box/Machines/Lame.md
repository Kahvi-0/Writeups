# Lame

![Title](https://user-images.githubusercontent.com/46513413/72587808-59d38000-38c4-11ea-9bb9-46105774f3f0.png)

### Recon and enumneration

I started with an namp scan

    nmap -p - -T4 -A -v 10.10.10.40
    
    -p-  scan all ports
    
    -T4 aggressive speed
    
    -A OS detection, service version scanning, script scanning and traceroute 
    
    -v verbose

![scan](https://user-images.githubusercontent.com/46513413/72587747-23960080-38c4-11ea-9bdc-ae66c4b9afda.png)


  The scan revealed ports and services: 
  
        21 vsftpd 2.3.4
        22 OpenSSH 4.7p1
        139 Samba 3.x - 4.x
        445 Samba 3.x - 4.x
        3632 Distccd v1 4.2.4
        
        
        
**vsftpd** I found a metasploit module for a vsftpd backdoor that I was unable to get a shell with.
  
![ftp2](https://user-images.githubusercontent.com/46513413/72588416-4aedcd00-38c6-11ea-804a-a21c0c027517.png)


**SSH** I decided to leave SSH for later if we are able to gather any information about any accounts.

**SAMBA**  I decided to run "auxiliary/scanner/smb/smb_version" to try and find the exact version. This revealed that the version of Samba running is 3.0.20-Debian.

![Samba1](https://user-images.githubusercontent.com/46513413/72588569-bfc10700-38c6-11ea-9150-79dbe25420f7.png)

I gave this version of Samba a quick look on CVEdetails and found a few high CVSS scores. The CVE-2012-1182 is a CVSS of 10 and is listed to have a metasploit module. 

![samba3](https://user-images.githubusercontent.com/46513413/72588570-c0599d80-38c6-11ea-8822-c5f91caed16c.png)

**Distccd** I was able to find the metasploit module "exploit/unix/misc/distcc_exec".

![distccd shell](https://user-images.githubusercontent.com/46513413/72588812-758c5580-38c7-11ea-8dee-2ffef1f4782c.png)






















