# UpdateScp

Updates the System Control Processor (SCP) firmware with the given SCP image file (e.g. `scp_image.tar` for OpenBMC).

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateScp --file <filename> --reboot [--post_complete]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c UpdateScp --file <filename> --reboot
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateScp --file <filename> --reboot [--post_complete]
```

## Options

- `--file <file name>`: Required. Updates the SCP with the given SCP image file
- `--reboot`: Required. Forces the managed system to reboot or power up after operation
- `--individually`: Updates each SCP with its corresponding firmware file individually

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateScp --file scp_image.tar --reboot
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateScp --file scp_image.tar --reboot
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateScp --file scp_image.tar
```

## Output

```
Managed system.....................192.168.34.56
 SCP FW version.................2.0a
Local SCP image file...............scp_image.tar
Status: Start updating SCP for 192.168.34.56
************************************WARNING*************************************
 Do not remove AC power from the server.
********************************************************************************
Powering off target system............Done
Uploading FW...Done
Updating FW.....................................................
............Done
Powering up target system............Done
Status: SCP is updated for 192.168.34.56
```

## Notes

- BMC only accepts tar firmware files for SCP firmware updates.
- When using SSH to run the in-band `UpdateScp` command, adjust SSH timeouts on both client and server to avoid a broken pipe; typical execution time is within 30 minutes, so the timeout should be longer than 30 minutes.
- SCP can only be updated while the system is powered off, so `--reboot` is required. For in-band updates, SAA powers off the system after uploading the image to start the update process, then powers it back on automatically once complete.
- In-band SCP updates can only be done through the Redfish Host Interface.
- The execution progress for the managed system is continuously updated to the "Execution Message" section of the managed system in the created log file.
