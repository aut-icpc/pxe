# English Guide for Serva

## A) Prerequisites
- Make sure SMBv1 is enabled (especially if you are running Serva in Windows 10).<br>
from Control Panel, go to Programs and then Turn Windows features on or off:
<p align="center">
  <img width=80% src="https://raw.githubusercontent.com/aut-icpc/pxe/master/images/1.png"></img>
</p>

find `SMB 1.0/CIFS File Sharing Support` and if it's not enabled, enable it:
<p align="center">
  <img width=50% src="https://raw.githubusercontent.com/aut-icpc/pxe/master/images/2.png"></img>
</p>

then, restart your system so that changes will be applied.
<br>

- If you are testing Serva is VMWare, put both server's and client's Network into `Host-only`:
<p align="center">
  <img width=80% src="https://raw.githubusercontent.com/aut-icpc/pxe/master/images/3.png"></img>
</p>

and then:
<p align="center">
  <img width=80% src="https://raw.githubusercontent.com/aut-icpc/pxe/master/images/4.png"></img>
</p>

## B) Serva Configuration
1. Extract the zip file.
2. Create a folder named 'root' next to `Serva64.exe` file (only if the folder doesn't already exist).
3. Run `Serva64.exe` and go to Setting.
4. In TFTP tab, Enable `TFTP Server` and choose the 'root folder as `TFTP Server root directory`. Don't change other fields:
<p align="center">
  <img width=40% src="https://raw.githubusercontent.com/aut-icpc/pxe/master/images/5.png"></img>
</p>

5. In DHCP tab, enable `proxyDHCP` and `BINL`. Don't change other fields:
<p align="center">
  <img width=40% src="https://raw.githubusercontent.com/aut-icpc/pxe/master/images/6.png"></img>
</p>

6. Hit OK, close Serva and run it again, so that changes will take place.

## C) ISO Configuration
1. Go to `root/NWA_PXE` and create a new folder named something like 'ubuntu'.<br>
**Note: If you want to have more that 1 OS, then make other folders in `root/NWA_PXE` and follow all the steps to the end of this guide, for those folders, too.**
2. Copy all the contents of your ISO (not the ISO itself!) to `root/NWA_PXE_/ubuntu`.
3. Go to `root/NWA_PXE/ubuntu/casper`, and change the extension of 'initrd' file to '.lz'.
4. Now you got you download the proper INITRD_N11.x.x.gz:
- for Ubuntu LTS 18.04 and higher, download this:
https://www.vercot.com/~serva/download/INITRD_N11.2.4.GZ
- for Ubuntu LTS 16.04 to before LTS 18.04, download this:
https://www.vercot.com/~serva/download/INITRD_N11.2.2.GZ
5. Place the downloaded file under the `root/NWA_PXE/ubuntu/casper` directory.

## D) ServaAsset.inf Configuration
1. Under `root/NWA_PXE/ubuntu/` create a file named 'ServaAsset.inf' (.inf is the extension!).
2. Open the file with a text editor and copy and paste the following lines into it:
```
[PXESERVA_MENU_ENTRY]
asset    = $OS_NAME$
platform = amd64
 
kernel = /NWA_PXE/$HEAD_DIR$/casper/vmlinuz
append = showmounts toram root=/dev/cifs initrd=/NWA_PXE/$HEAD_DIR$/casper/initrd.lz,/NWA_PXE/$HEAD_DIR$/casper/$INITRD$ boot=casper netboot=cifs nfsroot=//$IP_BSRV$/NWA_PXE_SHARE/$HEAD_DIR$ NFSOPTS=-ouser=$USERNAME$,pass=$PASSWORD$,sec=ntlm,vers=1.0,ro ip=dhcp ro ipv6.disable=1
```
3. Now you got to replace $$ values: (remove the $s too!)
- `$OS_NAME$` -> the OS name you want to see in boot menu.
- `$HEAD_DIR$` -> with the folder that you created in root/NWE_PXE (we named it 'ubuntu').
- `$INITRD$` -> `INITRD_N11.2.2.GZ` or `INITRD_N11.2.4.GZ` based on the file you downloaded.
- `$USERNAME$` and `$PASSWORD$` -> the username and password that you've logged in into Windows.
- `$IP_BSRV$` -> IP of your system in the current network. (run 'ipconfig' in cmd and find your IP:)
<p align="center">
  <img width=80% src="https://raw.githubusercontent.com/aut-icpc/pxe/master/images/7.png"></img>
</p>

4. Save the file and close it.
5. Close Serva and run it again for 1-2 times, so that you only see these 2 lines:
<p align="center">
  <img width=60% src="https://raw.githubusercontent.com/aut-icpc/pxe/master/images/8.png"></img>
</p>

## E) Sharing NWA_PXE:
1. Right click on NWA_PXE folder and go to Properties.
2. In Sharing tab, click on Advanced Sharing:
<p align="center">
  <img width=40% src="https://raw.githubusercontent.com/aut-icpc/pxe/master/images/9.png"></img>
</p>

3. Enable Share this folder and use `NWA_PXE_SHARE` as Share name:
<p align="center">
  <img width=40% src="https://raw.githubusercontent.com/aut-icpc/pxe/master/images/10.png"></img>
</p>

4. Hit OK and you are Done!

## Troubleshooting
- `Bad option -ouser`:
This is the most common error that you might get. So:
1. Check if you've done part A)Prerequisites.
2. Check if you've downloaded the right INITRD file and placed it in the corrent folder.
3. Check if you've changed the extension of inird file to .lz
4. Check if you've correctly entered IP, username and password in ServaAsset.inf.
5. Check if the options after username and password (sec=ntlm,vers=1.0,ro) exist.
5. Also, you can turn off Firewall.

**If you're still getting this error or any other errors, please read the documentations of Serva:
https://www.vercot.com/~serva/default.html**
