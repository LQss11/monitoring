# Windows Exporter
Similar to node exporter there is windows exporter that exports windows host metrics:
## Installation Steps
- Download msi from [releases page](https://github.com/prometheus-community/windows_exporter/releases)
- Install via UI from MSI or Run on powershell command 
```ps
# msiexec /i C:\Users\<User>\Downloads\windows_exporter-0.31.2-amd64.msi --% CONFIG_FILE="C:\Users\<User>\Desktop\monitoring\exporters\windows-exporter\config.yaml"
msiexec /i <path-to-msi-file> --% CONFIG_FILE="D:\config.yaml"
```
- Get logs
```ps
Get-EventLog -LogName Application -Source windows_exporter -Newest 20
```
## Uninstall windows exporter (run as admin)
In order to uninstall you need to run:
```ps
sc.exe delete windows_exporter
```
- Check if running
```
Get-Service windows_exporter
```

# References
- [windows_exporter github](https://github.com/prometheus-community/windows_exporter) 
- [Docker windows exporter image](https://hub.docker.com/r/prometheuscommunity/windows-exporter)