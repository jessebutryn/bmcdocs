# GetGpuERoTInfo

Gets the External RoT (ERoT) GPU firmware image information of NVIDIA MGX systems from the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetGpuERoTInfo
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetGpuERoTInfo
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetGpuERoTInfo
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetGpuERoTInfo
```

### In-Band Redfish Host Interface
```bash
[SAA_HOME]# ./saa -c GetGpuERoTInfo -I Redfish_HI -u ADMIN -p ADMIN
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetGpuERoTInfo
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

```
Managed system..........................192.168.34.56
 [GPU 0]
 ERoT version....................01.03.0103.0000_n01
```

## Notes

- This command is specific to NVIDIA MGX systems.
- The execution progress for the managed system is continuously updated in the Execution Message section of the created log file.
