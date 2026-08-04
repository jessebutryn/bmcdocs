# GetSPDMInfo

Gets and reads the SPDM (Security Protocol and Data Model) measurement information of the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetSPDMInfo --item <item_name> [--showall]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetSPDMInfo --item <item_name> [--showall]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetSPDMInfo --item <item_name> [--showall]
```

## Options

- `--item <item_name>`: Prints the measurements from the specified item. Item name: 1 = CPU, 2 = GPU.
- `--showall` (Optional): Prints all measurements.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetSPDMInfo --item CPU
```

### In-Band Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetSPDMInfo --item CPU --showall
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetSPDMInfo --item GPU
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

```
Managed system.....................172.30.102.144
Item...........................CPU
MeasurementSummary.............19E71EA9A1DD8CB7CD352A636C54CE30
 A8455B7EF494C83EC213340C6BCD7003
D8BC11B671D73146E7B09F33FDB22C08
Measurement(01)................0101070083040000000003
Measurement(02)................020107008304004E564300
Measurement(03)................03010400830100FF
Measurement(04)................04013300013000F3B4B4DD0B66A1A529
 83177E71C697904458ED0452C6431C26
5BE4FA9529D0A1E9983E864FCC74B665
88E66C5E53BAE9
```

### With --showall
```
Managed system..........................169.254.3.254
 MeasurementSummary..............B4CBFE417CFFF035582F075F970EFA59
 B9DB5231CED16E4EA5191FF60EE4935A
EAE75DCE02DD04993075F4ED9803C3B8
 Measurement(1)..................0101070083040000000003
 Measurement(2)..................020107008304004E564300
 Measurement(3)..................03010400830100FF
 Measurement(4)..................04013300013000F3B4B4DD0B66A1A529
 83177E71C697904458ED0452C6431C26
5BE4FA9529D0A1E9983E864FCC74B665
88E66C5E53BAE9
 Measurement(5)..................05013300013000F3B4B4DD0B66A1A529
83177E71C697904458ED0452C6431C26
5BE4FA9529D0A1E9983E864FCC74B665
88E66C5E53BAE9
 Measurement(6)..................06013300013000F3B4B4DD0B66A1A529
83177E71C697904458ED0452C6431C26
5BE4FA9529D0A1E9983E864FCC74B665
88E66C5E53BAE9
 Measurement(7)..................07013300013000000000000000000000
00000000000000000000000000000000
00000000000000000000000000000000
00000000000000
 Measurement(8)..................08013300013000000000000000000000
00000000000000000000000000000000
00000000000000000000000000000000
00000000000000
```

## Notes

- The execution progress for the managed system is continuously updated in the Execution Message section of the created log file.
