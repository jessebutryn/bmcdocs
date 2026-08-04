# UpdateTransitionboardCpld

Updates the Transitionboard CPLD on the managed system with the given Transitionboard CPLD firmware image.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateTransitionboardCpld --file <filename>
```

### In-Band
```
saa -I Redfish_HI -c UpdateTransitionboardCpld --file <filename>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateTransitionboardCpld --file <filename>
```

## Options

- `--file <file name>`: Updates the Transitionboard CPLD with the given CPLD image file.
- `--individually`: (Optional) Updates each Transitionboard CPLD with its corresponding image file individually.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateTransitionboardCpld --file Transboard_CPLD.jed
```

### In-Band Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateTransitionboardCpld --file Transboard_CPLD.jed
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateTransitionboardCpld --file Transboard_CPLD.jed
```

## Output

```
Managed system.....................192.168.34.56
 CPLD version...................00.00.00
Status: Start updating Transitionboard CPLD for 192.168.34.56
************************************WARNING*************************************
 Do not remove AC power from the server.
********************************************************************************
Uploading FW...Done
Preparing updating FW.........Done
Updating FW...>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>Done
Status: Transitionboard CPLD is updated for 192.168.34.56
Note: Update done. No further action is needed for this firmware to take effect.
```
