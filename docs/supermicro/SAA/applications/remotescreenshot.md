# RemoteScreenshot

Gets a screenshot of the remote managed system and saves it as a PNG file.

## Syntax

### Single System OOB
```
saa -i <IP or host name> -u <username> -p <password> -c RemoteScreenshot --file <filename.png> [--overwrite]
```

### Single System In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c RemoteScreenshot --file <filename.png> [--overwrite]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c RemoteScreenshot --file <filename.png> [--overwrite]
```

## Options

- `--file`: Saves the screen shot to a file.
- `--overwrite` (Optional): Overwrites the output file.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c RemoteScreenshot --file remotefile.png
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c RemoteScreenshot --file remotefile.png --overwrite
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c RemoteScreenshot --file remotefile.png
```

## Notes

- If the execution "Status" field of the managed system shows SUCCESS, the console output of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
