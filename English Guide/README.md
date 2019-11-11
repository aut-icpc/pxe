# English Guide for Serva

## A) Prerequisites
- Make sure SMBv1 is enabled (especially if you are running Serva in Windows 10).<br>
from Control Panel, go to Programs and then Turn Windows features on or off:
<p align="center">
  <img width=80% src="https://raw.githubusercontent.com/aut-icpc/pxe/master/images/1.png"></img>
</p>

find SMB 1.0/CIFS File Sharing Support and if it's not enabled, enable it:
<p align="center">
  <img width=50% src="https://raw.githubusercontent.com/aut-icpc/pxe/master/images/2.png"></img>
</p>

then, restart your system so that changes would be applied.
<br>

- If you are testing Serva is VMWare, put both server's and client's Network into Host-only:
<p align="center">
  <img width=80% src="https://raw.githubusercontent.com/aut-icpc/pxe/master/images/3.png"></img>
</p>

and then:
<p align="center">
  <img width=80% src="https://raw.githubusercontent.com/aut-icpc/pxe/master/images/4.png"></img>
</p
