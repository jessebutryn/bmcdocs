# SendDiagInterrupt

Sends a system diagnostic interrupt (NMI, Non-Maskable Interrupt) hardware interrupt to the managed system. In practice, this action may result in different behaviors across different operating systems.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SendDiagInterrupt
```

### In-Band
```
saa -c SendDiagInterrupt
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SendDiagInterrupt
```

## Options

None

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SendDiagInterrupt
```

### In-Band
```bash
[SAA_HOME]# ./saa -c SendDiagInterrupt
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SendDiagInterrupt
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

If the execution "Status" field for a managed system is SUCCESS, the BIOS and BMC capabilities of the managed system are shown in the "Execution Message" section in the created log file.
