# SNMP
## Linux
- Debian:
```sh
sudo apt install snmp -y
snmpwalk -v2c -c xxxx 192.168.1.1 1.3.6.1.2.1.1
snmpwalk -v3 -l authPriv -u SomeName -a MD5 -A SomeAuthPass -x DES -X SomePrivPass 192.168.1.1 1.3.6.1.2.1
```
- CentOS
```sh
sudo yum install net-snmp-utils -y   # for RHEL/CentOS
snmpwalk -v2c -c xxxx 192.168.1.1 1.3.6.1.2.1.1
snmpwalk -v3 -l authPriv -u SomeName -a MD5 -A SomeAuthPass -x DES -X SomePrivPass 192.168.1.1 1.3.6.1.2.1
```
## Windows
In windows there are several ways to test snmp, you can either 
- instal `snmpb` 
```sh
choco install snmpb
snmpb -> this will open snmpb GUI
```
- using `SnmpWalk` -> download from [this link](https://ezfive.com/snmpsoft-tools/snmp-walk/) 
```sh
# You can specify port using this -p:1611
.\SnmpWalk.exe -r:192.168.1.1 -t:10 -c:"xxxx" -os:.1.3.6.1.2.1.1.1.0 -op:.1.3.6.1.2.1.1.8.0
.\SnmpWalk.exe -r:"::1" -v:3 -sn:SomeName -ap:MD5 -aw:SomeAuthPass -pp:DES -pw:SomePrivPass -os:.1.3.6.1.2.1 -op:.1.3.6.1.2.65535 -q
```

# SNMP SIM
SNMP Sim emulates devices using captured SNMP data, sample files are available in this [LibreNMS repository](https://github.com/murrant/librenms-snmpsim/tree/master/captures) and more data could also be found once you install snmpsim under `/usr/local/snmpsim/data/`\

You can also generate a record of one of your devices by running this command:
```sh
docker run -it --rm  tandrup/snmpsim:latest bash -c "snmprec.py --agent-udpv4-endpoint=192.168.1.1 --use-getbulk --community=public --output-file=mydevice.snmprec --logging-method=null && cat mydevice.snmprec">snmpsim-data/mydevice.snmprec                                                           
```

# SNMP test
You can test by running 
```sh
docker-compose up -d
docker exec -it snmpd  bash -c "snmpwalk -v2c -c public snmpd" 
docker exec -it snmpd  bash -c "snmpwalk -v2c -c public snmpsim" 
```
# SNMP Setup (CISCO)

```sh
docker run -it --rm --net monitoring --cap-add=NET_ADMIN --device /dev/net/tun --name cisco-1700 -p 161:161 -v ${pwd}/c1700-adventerprisek9-mz.124-15.T14.bin:/c1700-adventerprisek9-mz.124-15.T14.bin:ro ichikawayukko/dynamips:v0.2.21-alpine -P 1700 -o 64 -r 128 -s 0:0:linux_eth:eth0 c1700-adventerprisek9-mz.124-15.T14.bin 
```

> You can download the ISOs from [here](https://www.sysnettechsolutions.com/en/cisco-ios-download-for-gns3/) 
### Enable SNMP
```sh
enable
# Setup IP  
enable
conf t
int FastEthernet0
ip address 172.20.0.30 255.255.0.0
no shut
end
show ip int brief
# Check snmp
show snmp
configure terminal
snmp-server community public RO
end
write memory
show running-config | include snmp
# ACL
configure terminal
access-list 10 permit 172.20.0.5
snmp-server community public RO 10
end
write memory
# Remove snmp
configure terminal
no snmp-server community myComString RO 10
end
write memory
```
