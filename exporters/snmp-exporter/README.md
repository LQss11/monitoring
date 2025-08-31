# SNMP Exporter
Export SNMP metrics, where it works in a way that you configure the auth and OIDs in snmp exporter, and then in prometheus query and url you can test and chose which params or auths you setup to use.
## Installation Steps
- Download msi from [releases page](https://github.com/prometheus-community/windows_exporter/releases)
> Since snmp exporter only provide executable and not installer file you will need to create service.

Once installed make sure to use the right url example:
```
http://localhost:9116/snmp?target=192.168.1.1
# You can also include multi modules
http://localhost:9116/snmp?module=ucd_la_table,arista_sw&target=192.168.1.1
```
### Config
The config can be found once snmp exporter installed, If running on docker/linux make sure it's under `/etc/snmp_exporter/snmp.yml`

In case you are trying to generate a config you can check the [snmp_exporter generator](https://github.com/prometheus/snmp_exporter/tree/main/generator) 


# Linux
You can follow this [Example tutorial for linux](https://sbcode.net/prometheus/snmp-exporter/) to setup snmp exporter as a service. Also check this [snmp_exporter.service](https://github.com/prometheus/snmp_exporter/blob/main/examples/systemd/snmp_exporter.service)
### Windows
You can use the simple service manager tool NSSM
```ps1
choco install nssm
$exePath = "C:\snmp_exporter\snmp_exporter.exe"
$configFile = "C:\snmp_exporter\snmp.yml"

# Install service
& nssm install snmp_exporter $exePath "--config.file=$configFile"
# Start service
nssm start snmp_exporter
# Service status
nssm status snmp_exporter
# Remove service 
nssm remove snmp_exporter
```
# References
- [snmp_exporter github](https://github.com/prometheus/snmp_exporter) 
- [Example tutorial linux](https://sbcode.net/prometheus/snmp-exporter/)