# UpdateMultinodeLcmc

Updates the multi-node LCMC firmware of a managed system with the given multi-node LCMC firmware image.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateMultinodeLcmc --file <filename> --reboot [--post_complete]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c UpdateMultinodeLcmc --file <filename> --reboot
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateMultinodeLcmc --file <filename> --reboot [--post_complete]
```

## Options

- `--file <file name>`: Updates the multi-node LCMC with the given multi-node LCMC image file.
- `--reboot`: Forces the managed system to reboot or power up after operation.
- `--post_complete`: (Optional) Waits for the managed system's POST to complete after reboot.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateMultinodeLcmc --file LCMC.jed --reboot --post_complete
```

### In-Band Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateMultinodeLcmc --file LCMC.jed --reboot
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateMultinodeLcmc --file LCMC.jed --reboot
```

## Output

```
Managed system.....................192.168.34.56
 LCMC version...................0.07
Status: Start updating Multi-node LCMC for 192.168.34.56
************************************WARNING*************************************
 Do not remove AC power from the server.
********************************************************************************
Uploading FW...Done
Updating FW...>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>Done
Status: The managed system 192.168.34.56 is waiting for POST complete
..........
Status: OEM
........................................
..................................................
..................................................
................................................
Status: The managed system 192.168.34.56 is POST completed
Status: Multi-node LCMC is updated for 192.168.34.56
```

## Notes

- The execution progress for the managed system is continuously updated in the "Execution Message" section of the managed system in the created log file.
