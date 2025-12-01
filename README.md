# Remote desktop on Debian WSL

First install the Debian WSL.

``` 
wsl --install Debian
```

To see which distros are online available type

```
wsl --list --online 
```

After the Debian WSL has started and you configured a user with a password update the wsl image:

```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt autoremove
```

## XRDP for a remote desktop connection

```
sudo apt update && sudo apt -y upgrade
sudo apt -y install cinnamon
sudo apt -y install cinnamon-desktop-environment
sudo apt -y install gnome
sudo apt -y install gnome-session
sudo apt -y install dbus-x11
sudo apt -y install xrdp
sudo cp /etc/xrdp/xrdp.ini /etc/xrdp/xrdp.ini.bak
sudo sed -i 's/3389/3390/g' /etc/xrdp/xrdp.ini
sudo sed -i 's/max_bpp=32/#max_bpp=32\nmax_bpp=128/g' /etc/xrdp/xrdp.ini
sudo sed -i 's/xserverbpp=24/#xserverbpp=24\nxserverbpp=128/g' /etc/xrdp/xrdp.ini
sudo /etc/init.d/xrdp start
```

```
sudo vi /etc/xrdp/startwm.sh
```

comment these lines to:
```
#test -x /etc/X11/Xsession && exec /etc/X11/Xsession
#exec /bin/sh /etc/X11/Xsession
```

and add these lines:
```
# cinnamon
dbus-update-activation-environment --all
cinnamon-session-cinnamon
```

I added the "dbus-update-activation-environment --all" because the gnome-terminal was not starting and it gave a "Time-out".

```
sudo systemctl start xrdp
sudo systemctl enable xrdp
```
