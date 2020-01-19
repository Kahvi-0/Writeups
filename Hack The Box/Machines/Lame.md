# Lame

![Title](https://user-images.githubusercontent.com/46513413/72587808-59d38000-38c4-11ea-9bb9-46105774f3f0.png)

## Recon and enumneration

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
        
        
        
**vsftpd** 

I found a metasploit module for vsftpd 2.3.4 backdoor code execution.
  
![ftp2](https://user-images.githubusercontent.com/46513413/72588416-4aedcd00-38c6-11ea-804a-a21c0c027517.png)


**SSH** 

I decided to leave SSH for later if we are able to gather any information about any accounts.

**SAMBA** 

I decided to run "auxiliary/scanner/smb/smb_version" to try and find the exact version. This revealed that the version of Samba running is 3.0.20-Debian.

![Samba1](https://user-images.githubusercontent.com/46513413/72588569-bfc10700-38c6-11ea-9150-79dbe25420f7.png)

I gave this version of Samba a quick look on CVEdetails and found a few high CVSS scores. The CVE-2012-1182 is a CVSS of 10 and is listed to have a metasploit module. 

![samba3](https://user-images.githubusercontent.com/46513413/72588570-c0599d80-38c6-11ea-8822-c5f91caed16c.png)


**Distccd** 

I was able to find the metasploit module "exploit/unix/misc/distcc_exec".



## Exploitation

### Using metasploit

**vsftpd** 

I attempted to use the metasploit module for vsftpd 2.3.4 backdoor code execution. I was unable to get a shell with this.

![vsftpd explout1](https://user-images.githubusercontent.com/46513413/72589319-e4b67980-38c8-11ea-9309-5ed53e08794b.png)

**distccd**

Trying the module I found for distccd got me a shell as daemon user, which does not have elevated privileges. I was only able to get the user flag. I wanted to try the other exploits prior to any privilege escalation exploits.

![72588812-758c5580-38c7-11ea-8dee-2ffef1f4782c](https://user-images.githubusercontent.com/46513413/72676031-7f928d80-3a5a-11ea-983d-2ed313a7094b.png)
**Samba**

Finally I tried multiple samba modules, including [CVE-2012-1182](https://www.rapid7.com/db/modules/exploit/linux/samba/setinfopolicy_heap), having no luck with a shell. Eventually I tried a module for [CVE-2007-2447](https://www.rapid7.com/db/modules/exploit/multi/samba/usermap_script), which is exploited by specifying a username containing shell meta characters, which then attackers can execute commands.

![samba 5](https://user-images.githubusercontent.com/46513413/72588572-c0599d80-38c6-11ea-9cd1-ee5ff1ada2c5.png)

![shell 1](https://user-images.githubusercontent.com/46513413/72589891-7a9ed400-38ca-11ea-93af-b2fca6924916.png)

This gave me a root shell :)

![shell 2](https://user-images.githubusercontent.com/46513413/72589892-7b376a80-38ca-11ea-8d45-de940267cb9a.png)

Moving to makis home directory reveals the user flag.

![flag 1](https://user-images.githubusercontent.com/46513413/72589888-7a9ed400-38ca-11ea-811d-f2bf7748961c.png)

Moving to /root directory reveals the root flag.

![flag 2](https://user-images.githubusercontent.com/46513413/72589890-7a9ed400-38ca-11ea-8359-c580da2fb28d.png)


### Manual exploitation


















