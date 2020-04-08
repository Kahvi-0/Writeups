# OWASP Juice Shop


## 1 Star challenges

**Confidential Document**

Looking for the usual robots.txt had one entry for /ftp. This ftp directory contained a file called "acquisitions.md". This file had informtaion about the companies upcoming acquisitions which can be very damaging.

**DOM XSS**

 The first area that I spotted with user input was the search function of the website. 
 
 I first tested with "\<h3>test</h3>" with successful results. 
 
 I put in the challenges requested XSS "\<iframe src="javascript:alert(`xss`)">" and an alert with xss popped up :)
  

**Error Handling**

I triggered this while testing for SQLi in the login input. 

**Missing Encoding**

**Outdated Whitelist**

**Privacy Policy**

The privacy policy is found under "Account -> Privay & Security -> Privacy Policy"

**Reflected XSS**

This was not available in the version I was running. 

**Repetitive Registration**

When submitting the account registration by either manipulating the local code or the POST request in transit if you change the "passwordRepeat" parameter to no match the "password" parameter, the account is still created successfully with the value of "password" meaning the site does not follow DRY. 

**Score Board**

This is *now* found on the sidebar of the website.

**Zero Stars**

If you intercept the POST request for the feedback submission, you can change "rating" to be 0. This is not an intended function of the site and proves poor user input validation.


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
