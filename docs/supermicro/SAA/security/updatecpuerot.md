# UpdateCpuERoT

Updates the CPU ERoT (External Root of Trust) firmware image on NVIDIA MGX systems.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateCpuERoT --file <filename>
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c UpdateCpuERoT --file <filename>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateCpuERoT --file <filename>
```

## Options

- `--file <file name>`: Updates the CPU ERoT with the given FW image file.
- `--individually`: Updates each CPU ERoT with the corresponding configuration file individually.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateCpuERoT --file CPU_ERoT.fwpkg
```

### In-Band Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p ADMIN -c UpdateCpuERoT --file CPU_ERoT.fwpkg
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateCpuERoT --file CPU_ERoT.fwpkg
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

The execution progress for the managed system is continuously updated in the Execution Message section of the created log file.

## Notes

- This command is specific to NVIDIA MGX systems.
