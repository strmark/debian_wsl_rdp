# WSL export and import

## WSL List

Check if the WSL is not running and ready to export

```
wsl --list --verbose
```

## WSL export

wsl --export <DistroName> <FileName> [Options]
```
wsl --export Debian c:\temp\debian.tar
```

## WSL import

wsl --import <NewDistroName> <InstallLocation> <FileName> [Options]

```
wsl --import Debian2 C:\WSL\Debian2 C:\temp\debian.tar --version 2
```

## Remove wsl

To remove a wsl: wsl --unregister <Distro> 

```
wsl --unregister Debian2
```
