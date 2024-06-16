# Network Automation Scripts

This repository contains scripts for automating network configurations using Tera Term macros.

## Features
- Automate OSPF configuration on routers
- Batch configuration of IP addresses on multiple interfaces
- Secure and efficient network management

## Requirements
- Tera Term installed on your system

## Usage
1. Clone the repository:
2. Open Tera Term and load the desired macro script.

## Examples
### OSPF Configuration Macro 
```ttl
; Tera Term Macro OSPF
host = '192.168.1.1'
port = '22'
username = 'admin'
password = 'password'
network_list = '192.168.10.0 0.0.0.255 area 0,192.168.20.0 0.0.0.255 area 0,192.168.30.0 0.0.0.255 area 0'
connect '/ssh2 /auth=password /user=' + username + ' /passwd=' + password + ' ' + host + ':' + port
wait 'login successful'
sendln 'enable'
wait '#'
sendln 'configure terminal'
wait '(config)#'
sendln 'router ospf 1'
wait '(config-router)#'
split(network_list, ",")
for i 0 to splitcount - 1
 network = item(i)
 sendln 'network ' + network
 wait '(config-router)#'
next
sendln 'exit'
wait '(config)#'
sendln 'exit'
wait '#'
disconnect

## Contribution
Feel free to fork this repository and contribute by submitting pull requests. For major changes, please open an issue first to discuss what you would like to change.

## License
[MIT](LICENSE)
