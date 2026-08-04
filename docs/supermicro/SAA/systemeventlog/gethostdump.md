# GetHostDump

Manages the managed system's host crash dump file: creates and downloads it, deletes it on the BMC, or downloads it directly from the BMC.

- Use `--action CreateDump` to create the managed system's crash dump file and download it from the BMC.
- Use `--action DeleteDump` to delete a crash dump file on the BMC.
- Use `--action DirectDump` to download the managed system's crash dump file directly from the BMC. If the crash dump file does not exist, SAA shows the warning "No dump messages exist, please create a dump message first."

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetHostDump --action <actiondump> [--file <HostDump.tgz> [--overwrite]]
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c GetHostDump --action <actiondump> [--file <HostDump.tgz> [--overwrite]]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetHostDump --action <actiondump> [--file <HostDump.tgz> [--overwrite]]
```

## Options

- `--action <action>`: Sets action to `1` = CreateDump, `2` = DeleteDump, `3` = DirectDump
- `--file <file name>`: Saves the crash dump data in a file. Required for both `--action CreateDump` and `--action DirectDump`
- `--overwrite`: Overwrites the output file

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetHostDump --action CreateDump --file HostDump.tgz --overwrite
```

### In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetHostDump --action 1 --file log.tgz
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetHostDump --action DeleteDump
```

## Notes

- The downloaded file is a compressed file saved in `.tgz` format.
- The `--file` option is required for both `--action CreateDump` and `--action DirectDump`.
- The `--action CreateDump` option is not available on H12 RoT platforms.
