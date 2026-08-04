# GetAocNICInfo

Gets the add-on NIC firmware information from the managed system, as well as add-on NIC local firmware image information (with the `--file` option).

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetAocNICInfo [--file <filename>] [--dev_id <add-on NIC device ID>]
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c GetAocNICInfo [--file <filename>] [--file_only] [--dev_id <add-on NIC device ID>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetAocNICInfo [--file <filename>] [--file_only] [--dev_id <add-on NIC device ID>]
```

## Options

- `--file <file name>`: Reads the AOC NIC firmware information from an input AOC_NIC image file.
- `--dev_id <DEVICE_ID>`: (Optional) AOC NIC device ID list.
- `--file_only`: (Optional) Works with the `--file` option, and only reads AOC-NIC information from the input image file.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetAocNICInfo --file AOC_NIC.bin
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetAocNICInfo --file AOC_NIC.bin --dev_id 1,2,3

[SAA_HOME]# ./saa -c GetAocNICInfo --file AOC_NIC.bin --file_only
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetAocNICInfo --file AOC_NIC.bin
```

## Output

```
Add-on Network Interface Card Information
=========================================
Managed system........... 192.168.34.56
AOC NIC ID...............[1]
[General]
 AOC NIC Description..NIC device (riser:RSC-W2-66G4)
 AOC NIC Manufacturer.Supermicro
 AOC NIC Model........AOC-S100GC-i2C
 AOC NIC S/N..........WA214S004412
 AOC NIC Part Number..AOC-S100GC-i2C
 AOC NIC DeviceType...Simulated
 AOC NIC FW version...3.00 (N:06008A7A)
[PCIeInterface]
 PCIe Type............Gen4
 Maximum PCIe Type....Gen4
 Lanes In Use.........16
 Maximum Lanes........16
AOC NIC ID...............[2]
[General]
 AOC NIC Description..NIC device (riser:RSC-W2-66G4)
 AOC NIC Manufacturer.Supermicro
 AOC NIC Model........AOC-S100GC-i2C
 AOC NIC S/N..........WA20CS001831
 AOC NIC Part Number..AOC-S100GC-i2C
 AOC NIC DeviceType...Simulated
 AOC NIC FW version...3.00 (N:06008A7A)
[PCIeInterface]
 PCIe Type............Gen4
 Maximum PCIe Type....Gen4
 Lanes In Use.........16
 Maximum Lanes........16
AOC NIC ID...............[3]
[General]
 AOC NIC Description..NIC device (riser:RSC-WR-6)
 AOC NIC Manufacturer.Supermicro
 AOC NIC Model........AOC-STG-b2T
 AOC NIC S/N..........HA209S003222
 AOC NIC Part Number..AOC-STG-b2T
 AOC NIC DeviceType...Simulated
 AOC NIC FW version...20.8.157.0
[PCIeInterface]
 PCIe Type............Gen3
 Maximum PCIe Type....Gen4
 Lanes In Use.........8
 Maximum Lanes........8
Local AOC NIC image file.AOC_NIC.bin
 AOC NIC FW version...2.40 (N:04A075E6)
```

## Notes

- Use the `GetAocNICInfo` command to check the existing device IDs on the managed system.
- For updatable Add-On NIC card chipsets, refer to the package file "PlatformFeatureSupportMatrix.pdf" or contact Supermicro technical support.
- If the execution "Status" field of the managed system shows SUCCESS, the console output of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
