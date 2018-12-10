**Google Cloud VM: How to install Ubuntu 18.04 (desktop environment) with teamviewer remote access**

1) Login to your google cloud console
2) Click on Resources - Computer Engine
3) Click on Create Instance
4) Click on SSH button to remote into the ubuntu instance
5) change the default user password by typing :
```bash
sudo passwd username (your username)
```
(we will need password to login to GUI later)

6) type:
```bash
sudo su -
```
   to become root

7) change the root user password as well type:
```bash
passwd
```

8) enable password for SSH login by edit the file: (not sure if this needed, but i just do that)
```bash
nano /etc/ssh/sshd_config

change PasswordAuthentication no
to PasswordAuthentication yes
add: PermitRootLogin yes

service ssh restart
```

9) type following command 1 by 1:
```bash
apt update
apt-get upgrade
apt-get install ubuntu-desktop ( require some time, please wait )
apt-get install xserver-xorg-video-dummy
```

10) edit the xorg conf:
```bash
nano /etc/X11/xorg.conf
```
add following:
```bash
Section "Device"
    Identifier  "Configured Video Device"
    Driver      "dummy"
EndSection
Section "Monitor"
    Identifier  "Configured Monitor"
    HorizSync 31.5-48.5
    VertRefresh 50-70
EndSection
Section "Screen"
    Identifier  "Default Screen"
    Monitor     "Configured Monitor"
    Device      "Configured Video Device"
    DefaultDepth 24
    SubSection "Display"
    Depth 24
    Modes "1600x900"
    EndSubSection
EndSection
```

11) reboot the server:
```bash
reboot
```
12) login as root again using:
```bash
sudo su -
```

13) install teamviewer:
```bash
apt install gdebi -y
cd /tmp
wget https://download.teamviewer.com/download/linux/teamviewer_amd64.deb
gdebi teamviewer_amd64.deb
teamviewer license accept
teamviewer daemon enable
teamviewer daemon start
teamviewer passwd thenewpassword
teamviewer info
```

on the teamviewer info you should able to get the teamviewer ID
and password use the password you set above.

View Recorded video at:

[![Ubuntu](http://img.youtube.com/vi/c8pXhTmxZRA/0.jpg)](https://youtu.be/c8pXhTmxZRA "Ubuntu")

Enjoy, dont forget to Like my video on Youtube :))
