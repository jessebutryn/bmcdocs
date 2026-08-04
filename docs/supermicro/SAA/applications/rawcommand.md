# RawCommand

Sends an IPMI or IPMB raw command to the target system.

## Syntax

### IPMI Raw Command

#### Single System OOB
```
saa -i <IP or host name> -u <username> -p <password> -c RawCommand --raw <raw command>
```

#### Single System In-Band
```
saa -c RawCommand --raw <raw command>
```

#### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c RawCommand --raw <raw command>
```

### IPMB Raw Command

#### Single System OOB
```
saa -i <IP or host name> -u <username> -p <password> -c RawCommand --ipmb <raw command>
```

#### Single System In-Band
```
saa -c RawCommand --ipmb <raw command>
```

#### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c RawCommand --ipmb <raw command>
```

## Options

- `--raw <raw command>`: Inputs hex-value commands.
- `--ipmb <raw command>`: Inputs hex-value commands.

## Examples

### IPMI Raw Command (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c RawCommand --raw '06 01'
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c RawCommand --raw '0x06 0x01'
```

### IPMI Raw Command (In-Band)
```bash
[SAA_HOME]# ./saa -c RawCommand --raw '06 01'
[SAA_HOME]# ./saa -c RawCommand --raw '0x06 0x01'
```

### IPMI Raw Command (Multiple Systems OOB)
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c RawCommand --raw '06 01'
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c RawCommand --raw '0x06 0x01'
```

### IPMB Raw Command (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c RawCommand --ipmb '00 2C 2E D3 57 01 00 10'
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c RawCommand --ipmb '0x00 0x2C 0x2E 0xD3 0x57 0x01 0x00 0x10'
```

### IPMB Raw Command (In-Band)
```bash
[SAA_HOME]# ./saa -c RawCommand --ipmb '00 2C 2E D3 57 01 00 10'
[SAA_HOME]# ./saa -c RawCommand --ipmb '0x00 0x2C 0x2E 0xD3 0x57 0x01 0x00 0x10'
```

## Output

### IPMI Raw Command
```
00
20 01 09 95 02 BF 7C 2A 00 7A 09 00 10 00 00
```

### IPMB Raw Command
```
00
57 01 00 4C 00
```

## Notes

- A raw command must be enclosed in quotation marks.
- If the execution "Status" field for a managed system is SUCCESS, the BIOS and BMC capabilities of the managed system will be shown in the "Execution Message" section in the created log file (multiple systems OOB usage).
