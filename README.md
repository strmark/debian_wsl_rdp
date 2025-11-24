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
cinnamon-session
```

I added the "dbus-update-activation-environment --all" because the gnome-terminal was not starting and it gave a "Time-out".

```
sudo systemctl start xrdp
sudo systemctl enable xrdp
```
## Optional 
The next steps are optional!
I describe how I added Docker, Zsh(oh-my-zsh) to the WSL.
 
### Installing Docker

```
# Add Docker's official GPG key:
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

```
# Add the repository to Apt sources:
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/debian
Suites: $(. /etc/os-release && echo "$VERSION_CODENAME")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF
```

```
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Additionally add the current user to the docker user so you can run docker as the user
```
sudo usermod -aG docker $USER
```

### Installing ZSH

I like oh-my-zsh as my enhanced terminal, so I installed zsh and oh-my-zsh. I also installed the powerline fonts for the agnoster zsh-theme.

```
sudo apt-get install zsh fonts-powerline

sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

I edited the .zshrc and changed the ``ZSH_THEME="agnoster"``
and ``plugins=( azure docker docker-compose git gradle helm kubectl mvn ng node npm nvm pip ubuntu )``

### Installing nvm (node version manager)

I installed the node version manager.

```
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```

### Installing Keychain

I installed keychain for the use of a ssh key with git and not having to type my password constantly.

```
sudo apt install keychain
```

### Additional Font installation

I downloaded a font from [jetbrains mono](https://www.jetbrains.com/lp/mono/)

Unpack fonts to ``~/.local/share/fonts or /usr/share/fonts`` (to install fonts system-wide) and after unpacking run ``fc-cache -f -v`` so the font can be found.
