How to update Lynis
===================

**After running nc-audit your might see the following and wonder how to update Lynis:**

`! Version of Lynis is very old and should be updated [LYNIS] 
      https://cisofy.com/controls/LYNIS/`

Well this is how you can update Lynis _(these instructions were slightly modified from [CISOfy](https://packages.cisofy.com/community/#debian-ubuntu))_

### 1. Import key from server
Copy and paste the line below and then hit enter.<br>
`sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C80E383C3DE9F082E01391A0366C67DE91CA5D5F`

After you hit enter, you should see this code output:
```
Executing: /tmp/apt-key-gpghome.1wEImqGOzn/gpg.1.sh --keyserver keyserver.ubuntu.com --recv-keys C80E383C3DE9F082E01391A0366C67DE91CA5D5F
gpg: key 366C67DE91CA5D5F: public key "CISOfy Software (signed software packages) <software@cisofy.com>" imported
gpg: Total number processed: 1
gpg:               imported: 1
```

### _Side note if you use your software in English:_
If you use your software in English, you can enter the following code to configure APT to skip downloading translations<br>

Copy and paste the line below and then hit enter.<br>
`echo 'Acquire::Languages "none";' | sudo tee /etc/apt/apt.conf.d/99disable-translations`

After you hit enter, you should see this code output:<br>
`Acquire::Languages "none";`

### 2. Add software repository
Copy and paste the line below and then hit enter.<br>
`echo "deb https://packages.cisofy.com/community/lynis/deb/ stable main" | sudo tee /etc/apt/sources.list.d/cisofy-lynis.list`

After you hit enter, you should see this code output:<br>
`deb https://packages.cisofy.com/community/lynis/deb/ stable main`

### 3. Run apt update
Copy and paste the line below and then hit enter.<br>
`sudo apt update`

After you hit enter, your code output will look similar to what is pasted below:<br>
```
Hit:1 http://archive.raspberrypi.org/debian stretch InRelease
Hit:2 http://raspbian.raspberrypi.org/raspbian stretch InRelease
Get:3 https://packages.cisofy.com/community/lynis/deb stable InRelease [11.4 kB]
Get:4 https://packages.cisofy.com/community/lynis/deb stable/main armhf Packages [672 B]
Fetched 12.1 kB in 1s (7,075 B/s)
Reading package lists... Done
Building dependency tree       
Reading state information... Done
7 packages can be upgraded. Run 'apt list --upgradable' to see them.
```

### 4. Run apt upgrade
Copy and paste the line below and then hit enter.<br>
`sudo apt upgrade`

After you hit enter, your code output will look similar to what is pasted below:<br>
```
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Calculating upgrade... Done
The following packages will be upgraded:
  libraspberrypi-bin libraspberrypi-dev libraspberrypi-doc libraspberrypi0 lynis raspberrypi-bootloader raspberrypi-kernel
7 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
Need to get 70.0 MB of archives.
After this operation, 105 kB of additional disk space will be used.
Do you want to continue? [Y/n]
```
Type y to continue and then hit enter.<br>
`y`
<br>After you hit enter, your code output will look similar to what is pasted below. Also, note I didn't paste all of the output because it was long)
```
Get:1 http://archive.raspberrypi.org/debian stretch/main armhf libraspberrypi-doc armhf 1.20180910-1 [31.4 MB]
Get:2 https://packages.cisofy.com/community/lynis/deb stable/main armhf lynis all 2.6.8-100 [216 kB]
...etc...
Preparing to unpack .../0-lynis_2.6.8-100_all.deb ...
Unpacking lynis (2.6.8-100) over (2.4.0-1) ...
dpkg: warning: unable to delete old directory '/etc/lynis/plugins': Directory not empty   
...etc...
Setting up lynis (2.6.8-100) ...
Installing new version of config file /etc/lynis/default.prf ...
Processing triggers for mime-support (3.60) ...
...etc...
Setting up libraspberrypi0 (1.20180910-1) ...
Setting up libraspberrypi-doc (1.20180910-1) ...
Setting up libraspberrypi-dev (1.20180910-1) ...
Setting up libraspberrypi-bin (1.20180910-1) ...
```

### 5. Check if Lynis has been updated
Copy and paste the line below and then hit enter.<br>
`lynis show version`

After you hit enter, you should see it list the latest version:<br>
'2.6.8'

### 6. You're done!

