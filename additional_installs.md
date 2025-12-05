# Additional installs 


The next steps are optional!
I describe i.e. how I added Docker, Zsh(oh-my-zsh) to the WSL.

## Zip, Curl and Wget

Be sure the following tools are available.

```
apt-get install zip curl wget vim
```
 
## Installing Docker

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

## Installing ZSH

I like oh-my-zsh as my enhanced terminal, so I installed zsh and oh-my-zsh. I also installed the powerline fonts for the agnoster zsh-theme.

```
sudo apt-get install zsh fonts-powerline

sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

I edited the .zshrc and changed the ``ZSH_THEME="agnoster"``
and ``plugins=( azure docker docker-compose git gradle helm kubectl mvn ng node npm nvm pip ubuntu )``

## Installing nvm (node version manager)

I installed the node version manager.

```
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```

## SDK-man

SDK-man
```
curl -s "https://get.sdkman.io" | bash
```
### Installing Keychain

I installed keychain for the use of a ssh key with git and not having to type my password constantly.

```
sudo apt install keychain
```

## Additional Font installation

I downloaded a font from [jetbrains mono](https://www.jetbrains.com/lp/mono/)

Unpack fonts to ``~/.local/share/fonts or /usr/share/fonts`` (to install fonts system-wide) and after unpacking run ``fc-cache -f -v`` so the font can be found.


## Deepin-terminal

```
apt-get install deepin-terminal
```

## Azure client
```
apt-get install azure-cli
```

## Python 3 installer

```
sudo apt install python3-pip
```
## K9S

```
wget https://github.com/derailed/k9s/releases/latest/download/k9s_linux_amd64.deb && apt install ./k9s_linux_amd64.deb && rm k9s_linux_amd64.deb
```

### Kubectl

```
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.34/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
sudo chmod 644 /etc/apt/keyrings/kubernetes-apt-keyring.gpg

echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.34/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo chmod 644 /etc/apt/sources.list.d/kubernetes.list
```

### btop

```
apt-get install btop
```
