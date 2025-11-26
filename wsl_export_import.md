# WSL export and impot

## WSL export

```
wsl --export Debian  c:\temp\debian.tar
```

### WSL import

```
wsl --import Debian2 C:\WSL\Debian2 C:\temp\debian.tar --version 2
```
