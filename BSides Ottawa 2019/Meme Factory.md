This is a web based challange that starts off with a page that lets the user upload a file.
There is a notcie stating that only .zip are allowed.

<a href="https://postimages.org/" target="_blank"><img src="https://i.postimg.cc/xTGh6btt/1.png" alt="1"/></a><br/><br/>

After a while of uploading files and watching the traffic to test the limits of this whilelist I noticed something while uploading a duplicate file with "(2).zip" in its name. 

<a href="https://postimages.org/" target="_blank"><img src="https://i.postimg.cc/hGvY4Zg5/2.png" alt="2"/></a><br/><br/>

Upload successful. The dev console shows that anything <space>( and past escaped the title that was given to the uploaded file but still pass the whitelist since .zip was present. Allowing F.php (2).zip to be uploaded as F.php. 

<a href="https://postimages.org/" target="_blank"><img src="https://i.postimg.cc/SRF1ry9B/4.png" alt="4"/></a><br/><br/>

This file also was just a basic php script proving that only the name is checked. 

<a href="https://postimages.org/" target="_blank"><img src="https://i.postimg.cc/3NXSfPCd/3.png" alt="3"/></a><br/><br/>

The site also shows exactly where to access my file and keeps the .php there. Now trying to access the php script with the added parameter allows us to run system commands and cat the flag.

<a href="https://postimages.org/" target="_blank"><img src="https://i.postimg.cc/SKPvnLxN/6.png" alt="6"/></a><br/><br/>
