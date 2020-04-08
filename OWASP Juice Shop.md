# OWASP Juice Shop


## 1 Star challenges

**Confidential Document**

Looking for the usual robots.txt had one entry for /ftp. This ftp directory contained a file called "acquisitions.md". This file had informtaion about the companies upcoming acquisitions which can be very damaging.

**DOM XSS**

 The first area that I spotted with user input was the search function of the website. 
 
 I first tested with "<h3>test</h3>" with successful results. 
 
 I put in the challenges requested XSS "<iframe src="javascript:alert(`xss`)">" and an alert with xss popped up :)
  

**Error Handling**

I triggered this while testing for SQLi in the login input. 

**Missing Encoding**

**Outdated Whitelist**

**Privacy Policy**

The privacy policy is found under "Account -> Privay & Security -> Privacy Policy"

**Reflected XSS**

This was not available in the version I was running. 

**Repetitive Registration**

**Score Board**

**Zero Stars**


## 2 Star challenges

**Admin Section**

**Classic Stored XSS**

**Deprecated Interface**

**Five-Star Feedback**

**Login Admin**

**Login MC SafeSearch**

**Password Strength**

**Security Policy**

**View Basket**

The locally stored cookie called "bid" controls the ID of the cart that you should be viewing. Chaning this value allows you to see other users carts. The value is just the number of the users basket in order of the user creation. The baskets are stored on the server under /rest/basket/<bid>

**Weird Crypto**
