![Easy Phish](https://user-images.githubusercontent.com/46513413/71924412-f24b6100-315c-11ea-9102-b9a8557cf4a8.png)

After seeing that "secure-startup.com" was a parked domain I ran a google search.

"domain: secure-startup" led me to a scan of the whois for "secure-startup.com" https://secure-startup.com.websiteoutlook.com/.
The first part of the flag is in the SPF record indicating that this is only one part as to why phishing using this domain has been easy.

![ez p 2](https://user-images.githubusercontent.com/46513413/71925014-22473400-315e-11ea-9348-f901e4822e03.png)


I started to research other ways to prevent spoofing and came across DMARC records in https://gatefy.com/posts/tips-protect-your-domain-and-prevent-email-spoof/. 

This lead me to trying to look at the sites DMARC record here: https://dmarcian.com/dmarc-inspector/. 
This revealed the second half of the flag, proving that DMARC was the other half of the reason that using this site for phishing is so easy.

![ez 3](https://user-images.githubusercontent.com/46513413/71925362-dd6fcd00-315e-11ea-8bb3-a12eed753482.png)


**SPF record:** SPF is an email verification and authentication tool that focuses on protection against spoofing. It allows you to determine IP addresses able to send emails using your domain. In other words, if the IP address doesn't match the domain, the email provider should block the message.

**DMARC record:** DMARC acts by standardizing the way emails are checked by servers. It uses SPF and/or DKIM to verify the sender and allows the domain owner to determine actions. For example, sending a message to the quarantine if it presents problems. In addition, DMARC allows domain owners to receive reports about emails that were delivered and/or failed.
