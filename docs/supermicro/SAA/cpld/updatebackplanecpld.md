# UpdateBackplaneCpld

Updates the backplane CPLD firmware of a managed system with the given backplane CPLD firmware image.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateBackplaneCpld {--index <BPN index> --file <filename> | --update_list <BPN index>:<filename>[,<BPN index>:<filename>...]} --manual_ejected
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateBackplaneCpld {--index <BPN index> --file <filename> | --update_list <BPN index>:<filename>[,<BPN index>:<filename>...]} --manual_ejected
```

## Options

- `--manual_ejected`: Confirms that all drives on the backplane have been ejected manually.
- `--file <file name>`: Updates the Backplane CPLD with the given FW image file.
- `--index <number>`: Updates the specific Backplane CPLD with the given index.
- `--dev_id <number>`: (Optional) Sets the CPLD index. The default value is 1.
- `--update_list <item list>`: (Optional) Updates multiple backplane CPLDs with one command, using a comma (",") to distinguish between items. Item list example: `1:CPLD.jed,2:CPLD.jed…`
- `--individually`: (Optional) Updates each backplane CPLD with its corresponding image file individually.
- `--upgrade_only`: (Optional) Firmware updates are only performed when the version is newer.
- `--check_reboot_required`: (Optional) Displays a warning message when a system reboot or power cycle is required.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateBackplaneCpld --index 0 --file BPN_CPLD.jed --manual_ejected
```

### OOB (multiple backplanes with --update_list)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateBackplaneCpld --update_list 0:BPN_CPLD.jed,1:BPN_CPLD.jed --manual_ejected
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -c UpdateBackplaneCpld --index 0 --file BPN_CPLD.jed --manual_ejected
```

## Output

```
Status: Start updating Backplane CPLD for 192.168.34.56
************************************WARNING****************************
Do not remove AC power from the server.
************************************************************************
Warning: All drives on backplane will be force ejected due to backplane reset after update.
Managed system......................192.168.34.56
 Backplane CPLD ID...............0023
 Backplane CPLD Revision.........0C
Local CPLD image file...............BPN_CPLD.jed
Uploading FW...Done
Updating FW...>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>Done
Status: Backplane CPLD is updated for 192.168.34.56
```

The execution progress for the managed system is continuously updated in the "Execution Message" section of the managed system in the created log file.
