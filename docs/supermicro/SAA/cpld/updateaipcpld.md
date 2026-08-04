# UpdateAipCpld

Updates the AIP (AI Processor) CPLD firmware of managed systems installed with AIP, using the given AIP CPLD firmware image. This command is OOB only.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateAipCpld --file <filename>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateAipCpld --file <filename>
```

## Options

- `--file <file name>`: Updates the CPLD of AIP with the given FW image file.
- `--individually`: (Optional) Updates each AIP CPLD with its corresponding image file individually.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateAipCpld --file AIP_CPLD.bin
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateAipCpld --file AIP_CPLD.bin
```

## Output

```
Managed system.....................192.168.34.56
 AIP FW version.................1A;1A;1A;1A;1A;1A;1A;1A
Local AIP image file...............AIP_CPLD.bin
Status: Start updating AIP CPLD for 192.168.34.56
************************************WARNING*************************************
 Do not remove AC power from the server.
********************************************************************************
Uploading FW.......Done
Updating FW...>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>Done
Status: AIP CPLD is updated for 192.168.34.56
Update Complete, Please wait for BMC reboot, about 5 mins.
..................................................
..................................................
..................................................
..................................................
..................................................
.............................................Done
```

## Notes

- This command is supported on the SYS-420GH-TNGR system.
- The execution progress for the managed system is continuously updated in the "Execution Message" section of the managed system in the created log file.
- This command is OOB only.
