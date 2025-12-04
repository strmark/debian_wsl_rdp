# Add google chrome

Get the key from google.
```
curl -fSsL https://dl.google.com/linux/linux_signing_key.pub | gpg --dearmor | sudo tee /usr/share/keyrings/google-chrome.gpg > /dev/null
```

Add it to the software repo of your machine
```
echo "Types: deb
URIs: https://dl.google.com/linux/chrome/deb/
Suites: stable
Components: main
Architectures: amd64
Signed-By: /usr/share/keyrings/google-chrome.gpg" | sudo tee /etc/apt/sources.list.d/google-chrome.sources
```

Update the software repository
```
sudo apt-get update
```

Check in /etc/apt/sources.list.d if google-chrome.sources and google-chrome.list exist. If so, remove the google-chrome.sources

```
sudo rm /etc/apt/sources.list.d/google-chrome.sources
```

Install google-chrome
```
sudo apt install google-chrome-stable
```
