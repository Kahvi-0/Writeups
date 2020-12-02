# TryHackMe Advent of Cyber 2020 - Day 1

## Web Exploitation

For the first day of the Advent of Cyber 2020 we are tasked with hacking back into Santa's account for the assembly line tool.

The first step is to register for an account. This seems to suggest that we are going to attempt something along the lines of broken access control.

![logins screen](https://user-images.githubusercontent.com/46513413/100818075-61860f80-3417-11eb-9329-38d284f30d81.png)

I watched the login via BURP and noticed this auth cookie and saved it for later.

![our auth](https://user-images.githubusercontent.com/46513413/100818076-621ea600-3417-11eb-9661-0c3fce01d88b.png)

Once I logged in I noticed that my user "elftest" has no ability to turn the systems back on.

![login no santa](https://user-images.githubusercontent.com/46513413/100818073-60ed7900-3417-11eb-9249-4ee23cdf3a08.png)

I decided to start with the cookie by throwing it into BURP's decider tool and trying to decode it. Surely enough, decoding it with ASCII hex made it readable.  

![decode](https://user-images.githubusercontent.com/46513413/100818066-6054e280-3417-11eb-8ef8-9f23433fc1b5.png)

Since we are trying to hack back into Santa's account, lets change my user "elftest" to "santa" and encode it back into ASCII hex.

![encode](https://user-images.githubusercontent.com/46513413/100818068-6054e280-3417-11eb-8bd4-78e3468fee83.png)

Now to replace the auth cookie for our user with the new cookie for the user "santa".

![adding cookie](https://user-images.githubusercontent.com/46513413/100818064-6054e280-3417-11eb-83b7-fe34713f230a.png)

Refresh the page . . . and we are now Santa's user!

![6](https://user-images.githubusercontent.com/46513413/100818062-5f23b580-3417-11eb-95ce-99d22f4e0b30.png)

Turning on all the systems will reveal the final flag.
