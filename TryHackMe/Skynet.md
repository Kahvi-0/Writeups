# SKYNET


## Reconnaissance

Runing NMAP reveals the following open ports/services:

    PORT    STATE SERVICE     VERSION
    22/tcp  open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
    | ssh-hostkey: 
    |   2048 99:23:31:bb:b1:e9:43:b7:56:94:4c:b9:e8:21:46:c5 (RSA)
    |   256 57:c0:75:02:71:2d:19:31:83:db:e4:fe:67:96:68:cf (ECDSA)
    |_  256 46:fa:4e:fc:10:a5:4f:57:57:d0:6d:54:f6:c3:4d:fe (ED25519)
    80/tcp  open  http        Apache httpd 2.4.18 ((Ubuntu))
    |_http-server-header: Apache/2.4.18 (Ubuntu)
    |_http-title: Skynet
    110/tcp open  pop3        Dovecot pop3d
    |_pop3-capabilities: RESP-CODES CAPA UIDL TOP SASL AUTH-RESP-CODE PIPELINING
    139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
    143/tcp open  imap        Dovecot imapd
    |_imap-capabilities: LITERAL+ LOGINDISABLEDA0001 IMAP4rev1 OK post-login more capabilities LOGIN-REFERRALS listed have ID Pre-login IDLE SASL-IR ENABLE
    445/tcp open  netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
    No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
    TCP/IP fingerprint:
    OS:SCAN(V=7.80%E=4%D=4/19%OT=22%CT=1%CU=40871%PV=Y%DS=2%DC=T%G=Y%TM=5E9CE16
    OS:2%P=x86_64-pc-linux-gnu)SEQ(SP=108%GCD=1%ISR=107%TI=Z%CI=I%II=I%TS=8)OPS
    OS:(O1=M54DST11NW7%O2=M54DST11NW7%O3=M54DNNT11NW7%O4=M54DST11NW7%O5=M54DST1
    OS:1NW7%O6=M54DST11)WIN(W1=68DF%W2=68DF%W3=68DF%W4=68DF%W5=68DF%W6=68DF)ECN
    OS:(R=Y%DF=Y%T=40%W=6903%O=M54DNNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=A
    OS:S%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R
    OS:=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F
    OS:=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%
    OS:T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD
    OS:=S)

    Network Distance: 2 hops
    Service Info: Host: SKYNET; OS: Linux; CPE: cpe:/o:linux:linux_kernel

    Host script results:
    |_clock-skew: mean: 1h39m59s, deviation: 2h53m12s, median: 0s
    |_nbstat: NetBIOS name: SKYNET, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
    | smb-os-discovery: 
    |   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
    |   Computer name: skynet
    |   NetBIOS computer name: SKYNET\x00
    |   Domain name: \x00
    |   FQDN: skynet
    |_  System time: 2020-04-19T18:40:14-05:00
    | smb-security-mode: 
    |   account_used: guest
    |   authentication_level: user
    |   challenge_response: supported
    |_  message_signing: disabled (dangerous, but default)
    | smb2-security-mode: 
    |   2.02: 
    |_    Message signing enabled but not required
    | smb2-time: 
    |   date: 2020-04-19T23:40:13
    |_  start_date: N/A


Running gobuster revealed the following directories: 

    /index.html 
    /admin 
    /ai 
    /config 
    /css 
    /js 
    /squirrelmail 
    /.htaccess 
    /.hta 
    /.htpasswd 
    /server-status 
    
    
## Services

**SMB**

Notable output from enum4linux.

     ======================================= 
    |    Share Enumeration on 10.10.2.29    |
     ======================================= 

            Sharename       Type      Comment
            ---------       ----      -------
            print$          Disk      Printer Drivers
            anonymous       Disk      Skynet Anonymous Share
            milesdyson      Disk      Miles Dyson Personal Share
            IPC$            IPC       IPC Service (skynet server (Samba, Ubuntu))
    SMB1 disabled -- no workgroup available

    [+] Attempting to map shares on 10.10.2.29
    //10.10.2.29/print$     Mapping: DENIED, Listing: N/A
    //10.10.2.29/anonymous  Mapping: OK, Listing: OK
    //10.10.2.29/milesdyson Mapping: DENIED, Listing: N/A
    //10.10.2.29/IPC$       [E] Can't understand response:
    NT_STATUS_OBJECT_NAME_NOT_FOUND listing \*
    
    S-1-5-21-2393614426-3774336851-1116533619-1000 SKYNET\milesdyson (Local User)
    
 We now have share list, share permissions and a valid system user.  

 We have anonymous access to the anonymous share.
 I downloaded all of the files in the share and found log files. 
 
 The log file titled log1.txt contains user passwords.
 
 
**HTTP**

The site itself is nothing special. The sites fundtions are either a POST request for either "Skynet+search" or "I;m Feeling Lucky" without the actual content of the search bar. 

  /squirrelmail - login page for SquirrelMail Login Webmail
  

## Gaining access

**Squirrel mail:**

Trying the system user **milesdyson** with the list of passwords from the log file reveals that **cyborg007haloterminator** is the valid password.

There are three emails in the inbox. The first one contains the milesdyson SMB share password )s{A&2Z=F^n_E.B\` . One of the other two is *"i can i i everything else . . . . . . . . . . . . . . balls have zero to me to me to me to me to me to me to me to me to"* and the other one is that phrase in binary.


**SMB**

Now that we know Miles' password, we are able to log into the milesdyson SMB share. The file notes/important.txt releaves a hidden directory the Miles has.

/45kra24zxs28v3yd


There was nothing special or manipulatable on this page. Running gobuster again on this directory shows that there is an administrator directory.



Running searchsploit for cuppa shows one RFI/LFI vulnerability.

 











