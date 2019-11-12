---
layout: default
---
<< [Home](./)

# Windows Index
* [Commands](#Useful-Commands)
* [Privilege Escalation](#Privilege-Escalation)

## Useful Commands<a name="Useful-Commands"></a>

...

## Privilege Escalation<a name="Privilege-Escalation"></a>

### List installed patches.

```bash
wmic qfe get Caption,Description,HotFixID,InstalledOn
```

### Find sensitive information.

Find files with certain keywords.
```bash
dir /s *pass* == *cred* == *vnc* == *.config*
```

Find certain file types with keyword.
```bash
findstr /si password *.xml *.ini *.txt
```

Find keywords in registry.
```bash
reg query HKLM /f password /t REG_SZ /s
reg query HKCU /f password /t REG_SZ /s
```

### Find unquoted service paths.
```bash
wmic service get name,displayname,pathname,startmode |findstr /i “Auto” |findstr /i /v “C:\Windows\\” |findstr /i /v “””
```