# UpdateDummySwitch

Updates the CMM dummy switch firmware on a managed system with the given image file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateDummySwitch {--file <filename> [--upload] | update <Apply>}
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateDummySwitch {--file <filename> [--upload] | update <Apply>} [--individually]
```

## Options

- `--file <file name>`: Updates the CMM dummy switch with the given image file (optional).
- `--upload`: Uploads the CMM dummy switch with the given image file only (optional).
- `--update <update rule>`: Updates the CMM dummy switch with the existing image on CMM. Supported update rule: `Apply` (optional).
- `--individually`: Updates each CMM dummy switch with its corresponding image file individually (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateDummySwitch --file DummySwitch.rom
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateDummySwitch --file DummySwitch.rom --upload
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateDummySwitch --update Apply
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateDummySwitch --file DummySwitch.rom
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateDummySwitch --file DummySwitch.rom --upload
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateDummySwitch --update Apply
```
