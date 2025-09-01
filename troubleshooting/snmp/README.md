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
.\SnmpWalk.exe -r:192.168.1.1 -t:10 -c:"xxxx" -os:.1.3.6.1.2.1.1.1.0 -op:.1.3.6.1.2.1.1.8.0
.\SnmpWalk.exe -r:"::1" -v:3 -sn:SomeName -ap:MD5 -aw:SomeAuthPass -pp:DES -pw:SomePrivPass -os:.1.3.6.1.2.1 -op:.1.3.6.1.2.65535 -q
```