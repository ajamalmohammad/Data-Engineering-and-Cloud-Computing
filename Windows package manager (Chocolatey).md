
1. Open Powershell terminal (Run as Administrator)
2. https://chocolatey.org/install 
```ps1
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

# install softwares

```BAT

choco install docker-desktop
choco install dbeaver-community

```

