# GetKcsPriv

Gets the current BMC KCS (Keyboard Controller Style) privilege level from the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetKcsPriv
```

### In-Band
```
saa -c GetKcsPriv
```

### Remote In-Band
```
saa -I Remote_INB --oi <OS IP address> --ou <OS username> --op <OS password> -c GetKcsPriv [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetKcsPriv
```

## Examples

### OOB
```bash
./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetKcsPriv
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetKcsPriv
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c GetKcsPriv
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetKcsPriv
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c GetKcsPriv
```

## Output

```
Managed system................192.168.34.56
 KCS Privilege Level.......4 (Administrator)
```
