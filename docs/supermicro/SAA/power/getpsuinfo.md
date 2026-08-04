# GetPsuInfo

Gets the current PSU information from the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetPsuInfo
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c GetPsuInfo
```

### Multiple Systems OOB
```
saa -l <system list file> -u <username> -p <password> -c GetPsuInfo
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetPsuInfo
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetPsuInfo
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetPsuInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetPsuInfo
```

## Output

### Via Redfish
```
[Module 1]:
 PWS Module Number: PWS-2K07A-1R
 PWS Serial Number: P2K7ACN32PB0126
 PWS Module Revision: 1.0
 Firmware Version: 1.0
 Status: OK
 AC Input Voltage: 116 V
 AC Input Current: 0.94 A
 DC 12V Output Voltage: 12.10 V
 DC 12V Output Current: 7.04 A
 Temperature 1: 40 C / 104 F
 Temperature 2: 62 C / 144 F
 Fan 1: 12448 RPM
 Fan 2: 0 RPM
 DC 12V Output Power: 85 W
 AC Input Power: 108 W
 Current Sharing Control: Active
```

### Via PMBus
```
[Module 1](SlaveAddress = 0xB0)
 PWS Module Number: PWS-2K09A-1R
 PWS Serial Number: P2K09CN53IB0413
 PWS Module Revision: 1.0
 PMBus Revision: 0x22
 Status: OK
 AC Input Voltage: 114.00 V
 AC Input Current: 0.98 A
 DC 12V Output Voltage: 12.15 V
 DC 12V Output Current: 7.38 A
 Temperature 1: 34 C / 93 F
 Temperature 2: 56 C / 133 F
 Fan 1: 6048 RPM
 Fan 2: 0 RPM
 DC 12V Output Power: 89 W
 AC Input Power: 111 W
 Current Sharing Control: Active - Active (90)
```

## Notes

- The console output may vary when getting PSU info through different interfaces, depending on the BMC version.
- If the execution Status field of the managed system shows SUCCESS, the console output of the managed system will be shown in the Execution Message section of the created log file.
