# UpdateMidplaneSbbCpld

Updates the Midplane Storage Bridge Bay (SBB) CPLD firmware of managed systems installed directly on the NVMe backplane, using the given CPLD firmware image.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateMidplaneSbbCpld --file <filename> --index <id> --reboot [--post_complete]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateMidplaneSbbCpld --file <filename> --index <id> --reboot [--post_complete]
```

## Options

- `--file <file name>`: Updates the Midplane SBB CPLD with the given CPLD image file.
- `--reboot`: Forces the managed system to reboot or power up after operation.
- `--index <number>`: Sets the CPLD index.
- `--post_complete`: (Optional) Waits for the managed system's POST to complete after rebooting.
- `--individually`: (Optional) Updates each Midplane SBB CPLD with its corresponding image file individually.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateMidplaneSbbCpld --file MidplaneSBB_CPLD.jed --index 1 --reboot --post_complete
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateMidplaneSbbCpld --file MidplaneSBB_CPLD.jed --index 1 --reboot
```

## Output

```
Managed system.....................192.168.34.56
 Midplane SBB CPLD 1 version....CPLD_ID: 0000 REV: 02
Local CPLD image file..............MidplaneSBB_CPLD.jed
Status: Start updating Midplane SBB CPLD for 192.168.34.56
************************************WARNING*************************************
 Do not remove AC power from the server.
********************************************************************************
Uploading FW...Done
Preparing updating...................Done
Updating FW...>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>Done
Rebooting target system.................................................Done
Status: The managed system 192.168.34.56 is waiting for POST complete
......
Status: MemoryInitializationStarted
.......................................
Status: PCIResourceConfigStarted
.....
.................
Status: The managed system 192.168.34.56 is POST completed
Status: Midplane SBB CPLD is updated for 192.168.34.56
```

## Notes

- This command is supported on systems equipped with a Midplane board.
