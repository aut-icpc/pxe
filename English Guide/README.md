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

then, restart your system so that changes will be applied.
<br>

- If you are testing Serva is VMWare, put both server's and client's Network into Host-only:
<p align="center">
  <img width=80% src="https://raw.githubusercontent.com/aut-icpc/pxe/master/images/3.png"></img>
</p>

and then:
<p align="center">
  <img width=80% src="https://raw.githubusercontent.com/aut-icpc/pxe/master/images/4.png"></img>
</p>

## B) Serva Configuration
1. Extract the Serva zip file.
2. Create a folder named 'root next to serva64.exe file (only if the folder doesn't already exist)
3. Run Serva63.exe ang go to Setting
4. In TFTP tab, Enable TFTP Server and choose the 'root' folder as TFTP Server root directory. Don't change the other fields:
<p align="center">
  <img width=40% src="https://raw.githubusercontent.com/aut-icpc/pxe/master/images/5.png"></img>
</p

5. In DHCP tab, enable proxyDHCP and BINL. Don't change other fields:
<p align="center">
  <img width=40% src="https://raw.githubusercontent.com/aut-icpc/pxe/master/images/6.png"></img>
</p

6. Hit OK, close Serva and run it again, so that changes will take place.

## C) ISO Configuration
1. Go to root/NWA_PXE and create a new folder named something like 'ubuntu'.
2. Copy all the contents of your ISO (not the ISO itself!) to root/NWA_PXE_/ubuntu.
3. Go to root/NWA_PXE/ubuntu/casper, and change the extension of 'initrd' file to '.lz'.
4. Now you got you download the proper INITRD_N11.x.x.gz:
- for Ubuntu LTS 18.04 and higher, download this:
https://www.vercot.com/~serva/download/INITRD_N11.2.4.GZ
- for Ubuntu LTS 16.04 to before LTS 18.04, download this:
https://www.vercot.com/~serva/download/INITRD_N11.2.2.GZ
5. Place the downloaded file under the root/NWA_PXE/ubuntu/casper directory.
