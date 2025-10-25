# GetAocNICInfo

Gets add-on NIC (Network Interface Card) firmware information from the managed system and/or local firmware image.

## Syntax

```
sum [[-i <IP or host name> | -I Redfish_HI] -u <username> -p <password>] -c GetAocNICInfo [--file <filename>] [--file_only] [--dev_id <add-on NIC device ID>]
```

## Options

- `--file <filename>`: Reads AOC NIC information from an input firmware image file
- `--file_only`: Works with `--file`, reads AOC NIC information from the input image file only
- `--dev_id <add-on NIC device ID>`: Specific device IDs to query (comma-separated)

## Examples

### OOB
```bash
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetAocNICInfo --file AOC_NIC.bin
```

### In-Band
```bash
[SUM_HOME]# ./sum -I Redfish_HI -u ADMIN -p PASSWORD -c GetAocNICInfo --file AOC_NIC.bin --dev_id 1,2,3
```

## Output

The console output includes information for each AOC NIC device:

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
```

## Notes

- Requires SFT-DCMS-SINGLE license
- Supported for both OOB and in-band usage
- Use `--dev_id` to query specific device IDs
