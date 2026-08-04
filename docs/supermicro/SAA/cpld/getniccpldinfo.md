# GetNICCpldInfo

Gets the NIC CPLD firmware image information from the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetNICCpldInfo
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetNICCpldInfo
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetNICCpldInfo
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetNICCpldInfo
```

### In-Band Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetNICCpldInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetNICCpldInfo
```

## Output

```
Managed system................ 192.168.34.56
 [NIC 1]
 [CPLD 1]
 CPLD Name.........NIC1 CPLD 1 System Slot A1 AOC-A200G-B2CM
 CPLD ID...........32E8
 CPLD Rev..........02
```

```
Managed system................ 169.254.3.254
 [NIC 1]
 [CPLD 1]
 CPLD Name.........NIC1 CPLD 1 System Slot A1 AOC-A200G-B2CM
 CPLD ID...........32E8
 CPLD Rev..........02
```
