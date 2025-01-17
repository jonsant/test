---
layout: default
---
<< [Home](./)

# Windows Index
* [Useful Commands](#Useful-Commands)
* [Privilege Escalation](#Privilege-Escalation)

## Useful Commands<a name="Useful-Commands"></a>

### Firewall

Disable:
```cmd
netsh advfirewall set  currentprofile state off
```

### RDP

Enable (requires admin rights):
```cmd
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f
```

Disable:
```cmd
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 1 /f
```

## Privilege Escalation<a name="Privilege-Escalation"></a>

### List installed patches.

```cmd
wmic qfe get Caption,Description,HotFixID,InstalledOn
```

### Find unquoted service paths.
```cmd
wmic service get name,displayname,pathname,startmode |findstr /i “Auto” |findstr /i /v “C:\Windows\\” |findstr /i /v “””
```

### See access rights on services (using sysinternals [accesschk.exe](https://docs.microsoft.com/en-us/sysinternals/downloads/accesschk))
```cmd
accesschk.exe /accepteula -uwcqv "Authenticated Users" *
```

### Find sensitive information.

Find files with certain keywords.
```cmd
dir /s *pass* == *cred* == *vnc* == *.config*
```

Find certain file types with keyword.
```cmd
findstr /si password *.xml *.ini *.txt
```

Find keywords in registry.
```cmd
reg query HKLM /f password /t REG_SZ /s
reg query HKCU /f password /t REG_SZ /s
```

### See file/folder permissions.
```cmd
icacls [path]
```
More on icacls at [microsoft](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/icacls).
