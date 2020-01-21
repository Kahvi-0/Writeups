# Netmon

![Title](https://user-images.githubusercontent.com/46513413/72780437-d92ac180-3bec-11ea-8702-adf7c7e52058.png)

## Recon and enumneration

Inital port scan:

    nmap -p - -T4 -A -v 10.10.10.40
    
    -p-  scan all ports
    
    -T4 aggressive speed
    
    -A OS detection, service version scanning, script scanning and traceroute 
    
    -v verbose
    
    
 **Scan results:**
 ![Scan 1](https://user-images.githubusercontent.com/46513413/72780315-923ccc00-3bec-11ea-9f26-969dfa6ae3b6.png)
 
 ![scan 2](https://user-images.githubusercontent.com/46513413/72780312-923ccc00-3bec-11ea-8431-adb967076f02.png)

 
 ## Enumeration notes for each discovered service 
 
 **FTP** - Anonymous access to windows root directory
           - Can access the user Public directory but not the administartor. Was able to access the user flag.
           
 ![ftp userflag](https://user-images.githubusercontent.com/46513413/72780325-92d56280-3bec-11ea-9ebb-1a55492d56c7.png)
 
 **HTTP** - PRTG network monitor version 18.1.37.139
           
    - Searching this version of PRTG had top results for clear text passwords being stored in a file called "PRTG Configuration.dat". 
           
    - Reasearched locations of where this file is stored, results were:
        - C:\ProgramData\Paessler\PRTG Network Monitor\Configuration Auto-Backups\
        - C:\ProgramData\Paessler\PRTG Network Monitor\PRTG Configuration.old
        - C:\ProgramData\Paessler\PRTG Network Monitor\PRTG Configuration.nul
                
    - There is an OS command injection associated with this version of PRTG (CVE-2018-9276) for users with access to the admin web console.
 

 ## Inital plan
 
  1. Access the server with the anonymous FTP login, leverage its large directory access and try to grab "PRTG Configuration.dat" 
  2. Use the clear text credentials to log into the web console.
  3. Run an exploit for CVE-2018-9276. 
 
 
 ## Exploitation
 
### Manual exploitation
 
  Using FTP I attempted to locate the C:\ProgramData directory with the "dir", however had no luck. I thought maybe this was an attempt of throwing me off. I snooped around and came across a copy of "PRTG Configuration.dat" in the C:\Windows directory. I downloaded a copy of it and started parsing. 
  
  After about 2-3 hours of not coming across anything in the XML wasteland that is "PRTG Configuration.dat" I started to doubt that I had the correct file and maybe this was a corrected/unaffected version. Going back I decied to try ls -la on C:/ for the hell of it, and would'nt you belive it, C:\ProgramData showed up. I found the files I needed. 
  
  ![PRTG 4](https://user-images.githubusercontent.com/46513413/72780322-92d56280-3bec-11ea-97f9-b54dafeb6743.png)

I notced that the .dat and .old were the same size as the one I already had, however the .old.bak was a different size. I downloaded that and discovered the user creds by searching the PRTG default username: prtgadmin.

  ![PRTG 5](https://user-images.githubusercontent.com/46513413/72780321-92d56280-3bec-11ea-850d-6b480280bb63.png)

trying to use these credentials in the web console however did not work. This confused me for a but until I realized that if the working .dat is corrected, then the admin would have been aware of this and changed their password. But what if the admin has bad password hygine . . . so I tried password: PrTg@admin2019. 

  . . . I was in to the admin console. 
    
   ![prtg6](https://user-images.githubusercontent.com/46513413/72780320-92d56280-3bec-11ea-8e34-e4a5d9ab6a2e.png)
   
It was now time to try and exploit CVE-2018-9276. I used the exploit updated by wildkindcc and originally created by M4LV0. 

  ![prtg 6](https://user-images.githubusercontent.com/46513413/72780318-92d56280-3bec-11ea-8e23-e573001838f9.png)
  
  ![prtg pwn](https://user-images.githubusercontent.com/46513413/72780317-923ccc00-3bec-11ea-89fb-3670608a8216.png)

 The exploit was successful. Root access :)

  ![root](https://user-images.githubusercontent.com/46513413/72780316-923ccc00-3bec-11ea-94ec-d1c89efbd431.png)
   

