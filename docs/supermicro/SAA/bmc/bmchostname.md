# BmcHostName

Gets and sets the BMC host name.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c BmcHostName --action <action> [--hostname <hostname>]
```

### In-Band
```
saa -c BmcHostName --action <action> [--hostname <hostname>]
```

### Remote In-Band
```
saa -I Remote_INB --oi <OS IP address> --ou <OS username> --op <OS password> -c BmcHostName --action <action> [--hostname <hostname>] [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c BmcHostName --action <action> [--hostname <hostname>]
```

## Options

- `--action <action>`: Required. Sets action: `1` = Get, `2` = Set
- `--hostname <Host Name>`: The host name (used with `--action Set`)

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c BmcHostName --action Get
```

### In-Band
```bash
[SAA_HOME]# ./saa -c BmcHostName --action Get
[SAA_HOME]# ./saa -c BmcHostName --action Set --hostname testHostName
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c BmcHostName --action Get --remote_saa /root/saa
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c BmcHostName --action Set --hostname testHostName --remote_saa /root/saa
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c BmcHostName --action Get
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c BmcHostName --action Set --hostname testHostName
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c BmcHostName --action Get
```

## Output

```
Managed system................192.168.34.56
 Host name................testHostName
```
