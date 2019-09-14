# Low Sodium Bagle
The second forensics challenege. Worth 300 points.

The image low-sodium-bagel.jpeg was provided for this challenge.

[![low-sodium-bagel.jpg](https://i.postimg.cc/vmqNL0fV/low-sodium-bagel.jpg)](https://postimg.cc/B8FpJchS)


I spent a long time messing with the colours in Gimp and going through a hex editor with no luck.
Eventually I tried steghide to detect any hidden files within the image.

[![1.png](https://i.postimg.cc/xCFqM37s/1.png)](https://postimg.cc/jwPsrPRN)

Sure enough it detected stegenopayload4837.txt.
used steghide -sf low-sodiu-bagel.jpeg to extract the hidden file

[![2.png](https://i.postimg.cc/3wtwQZKK/2.png)](https://postimg.cc/rdtTSx0b)

Opening stegenopayload4837.txt revealed the flag. 

[![3.png](https://i.postimg.cc/LXqgyWzd/3.png)](https://postimg.cc/wypBM0fF)
