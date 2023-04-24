# Ubuntu-SNMP-service
## Ubuntu  install and configure the SNMP service
### 1-Install the SNMP service
```
sudo apt install snmpd
```
### 2-Configuring SNMP service on Ubuntu
```
sudo nano /etc/snmp/snmpd.conf
```
### In the configuration file find the line below and comment out using # before
```
agentaddress 127.0.0.1,[::1]
```
### Then add the following line below so that the snmp service listens to all the IPv4 addresses of the server:
```
agentaddress udp:161,udp6:[::1]:161
```
<img src="https://user-images.githubusercontent.com/66946245/232918724-455979f4-f916-453c-bbb9-240746bac791.png" alt="Alt text" title="Optional title">

#### Now, we will add an SNMPV1 / SNMPv2C community in read-only (view).
The basic syntax is as follows:
```
rocommunity  default
```
In this way the community created will be accessible by everyone, to limit access to a network or an IP address, you must replace default by a CIRD notation.
```
rocommunity CommunityName 192.168.1.10/32
```
This way, the community will only be accessible to hardware with the IP address 192.168.1.10
It is especially important to apply an IP restriction if monitoring a web server at a provider.

<img src="https://user-images.githubusercontent.com/66946245/232919591-be069ec4-bbf1-4266-aab8-e73ea20f2941.png" alt="Alt text" title="Optional title">

Save and close the file (ctrl + x).

You must now restart the SNMP service to take the configuration into account.
```
sudo systemctl restart snmpd.service
```
