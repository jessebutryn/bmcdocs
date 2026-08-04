# UpdateMultinodeEc

Updates the multi-node EC firmware of a managed system with the given multi-node EC firmware image.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateMultinodeEc --file <filename>
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c UpdateMultinodeEc --file <filename>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateMultinodeEc --file <filename>
```

## Options

- `--file <file name>`: Updates the multi-node EC with the given multi-node EC image file.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateMultinodeEc --file EC.bin
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateMultinodeEc --file EC.bin
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateMultinodeEc --file EC.bin
```

## Output

```
Managed system.....................169.254.3.254
 EC ID..........................A7
 EC version.....................1.20
Local EC image file................EC.bin
 EC ID..........................A7
 EC Version.....................1.20

Status: Start updating Multi-node EC for 169.254.3.254
************************************WARNING*************************************
 Do not remove AC power from the server.
********************************************************************************
Uploading FW...Done
Updating FW...>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>Done
Status: Multi-node EC is updated for 169.254.3.254
```

## Notes

- The execution progress for the managed system is continuously updated in the "Execution Message" section of the managed system in the created log file.
