# DcmiManage

Manages the system through the Data Center Manageability Interface (DCMI) for Supermicro platforms. Supports the standard DCMI specification (`--type STD_DCMI`) and Intel Node Manager version 2.0 (`--type NM20`).

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c DcmiManage --type <STD_DCMI|NM20> --action <action> [options...]
```

### In-Band
```
saa -c DcmiManage --type <STD_DCMI|NM20> --action <action> [options...]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c DcmiManage --type <STD_DCMI|NM20> --action <action> [options...]
```

## Actions

Actions supported by `--type STD_DCMI` (Standard DCMI specification):

- **Find**: Finds DCMI devices from local or an IP range. In-band only.
- **GetCap**: Lists DCMI capabilities information.
- **GetPowerStatus**: Displays DCMI power reading information.
- **GetMCID**: Lists the management controller identifier string.
- **SetMCID**: Sets the management controller identifier string.
- **GetAssetTag**: Gets the asset tag string.
- **SetAssetTag**: Sets the asset tag string.

Actions supported by `--type NM20` (Intel Node Manager 2.0):

- **GetCap**: Gets DCMI capability information.
- **GetPowerReading**: Gets a power reading.
- **GetPowerLimit**: Gets the power limit.
- **SetPowerLimit**: Sets the power limit.
- **EnablePowerLimit**: Enables the power limit.
- **DisablePowerLimit**: Disables the power limit.

## Options

- `--type <type>`: `STD_DCMI` or `NM20`.
- `--action <action>`: The action to perform (see Actions above).
- `--start_ip <Start IP>`: Start IPv4 address, used with `Find` (optional).
- `--end_ip <End IP>`: End IPv4 address, used with `Find` (optional).
- `--netmask <Netmask>`: Netmask, used with `Find` (optional).
- `--value <Value>`: MCID or asset tag string value, used with `SetMCID`/`SetAssetTag`.
- `--mode <Mode>`: Power reading mode, used with `GetPowerReading`. `1` = System Power Statistics, `2` = Enhanced System Power Statistics.
- `--limit <Limit>`: Power limit in watts, used with `SetPowerLimit`.
- `--period <Period>`: For `GetPowerReading`, the rolling average time period (hex value obtained from `GetCap`). For `SetPowerLimit`, the management application statistics sampling period in seconds (optional).
- `--exception_action <Exception action>`: Used with `SetPowerLimit`. `0` = No Action, `1` = Hard power off system and log event to SEL, `17` = Log event to SEL.
- `--time <Time>`: Correction time limit in milliseconds, used with `SetPowerLimit`.

## Examples

### Find (In-Band only)
```bash
[SAA_HOME]# ./saa -c DcmiManage --type STD_DCMI --action Find --start_ip 192.168.34.1 --end_ip 192.168.34.100 --netmask 255.255.255.0
```

### GetCap (STD_DCMI)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c DcmiManage --type STD_DCMI --action GetCap
```

### GetPowerStatus (STD_DCMI)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c DcmiManage --type STD_DCMI --action GetPowerStatus
```

### GetMCID / SetMCID
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c DcmiManage --type STD_DCMI --action GetMCID

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c DcmiManage --type STD_DCMI --action SetMCID --value example
```

### GetAssetTag / SetAssetTag
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c DcmiManage --type STD_DCMI --action GetAssetTag

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c DcmiManage --type STD_DCMI --action SetAssetTag --value example
```

### GetCap (NM20)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c DcmiManage --type NM20 --action GetCap
```

### GetPowerReading (NM20)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c DcmiManage --type NM20 --action GetPowerReading --mode 2 --period 05
```

### GetPowerLimit / SetPowerLimit (NM20)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c DcmiManage --type NM20 --action GetPowerLimit

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c DcmiManage --type NM20 --action SetPowerLimit --exception_action 1 --limit 200 --time 20000 --period 50
```

### Enable/Disable Power Limit (NM20)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c DcmiManage --type NM20 --action EnablePowerLimit

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c DcmiManage --type NM20 --action DisablePowerLimit
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c DcmiManage --type STD_DCMI --action GetCap
```

## Output

### Find
```
Finding DCMI Devices ....................
 192.168.34.1 DCMI Ver:1.1
 192.168.34.2 DCMI Ver:1.1
 192.168.34.3 DCMI Ver:1.1
3 DCMI device(s) found
```

### GetCap (STD_DCMI)
```
DCMI Version = 1.1
Mandatory Platform capabilities
Temperature Monitor :Compliant
Chassis Power :Compliant
SEL logging :Compliant
Identification Support :Compliant
Optional Platform capabilities
Power Management :Compliant
Manageability Access Capabilities
VLAN Capable :Available
SOL Supported :Available
OOB Primary LAN Channel Available :Available
OOB Secondary LAN Channel Available :Not present
OOB Serial TMODE Available :Not present
In-Band KCS Channel Available :Available
SEL Attributes
SEL automatic rollover enabled :Not present
Number of SEL entries :0
Identification Attributes
Asset Tag Support :Available
DHCP Host Name Support :Not present
GUID Support :Available
Temperature Monitoring
Baseboard temperature :At least 1
Processors temperature :At least 1
Inlet temperature :At least 1
Power Management Device Slave Address
7-bit I2C Slave Address of device on IPMB :10
Power Management Controller Channel Number
Channel Number :00
Device Revision :01
Manageability Access Attributes
Mandatory Primary LAN OOB Support(RMCP+ Support Only) :supported
Optional Secondary LAN OOB Support(RMCP+ Support Only):Not supported
Optional Serial OOB TMODE Capability :Not supported
```

### GetPowerStatus (STD_DCMI)
```
Instantaneous power reading | 121 W
Minimum during sampling period | 65 W
Maximum during sampling period | 482 W
Average during sampling period | 123 W
IPMI timestamp | 2023/08/28 07:29:10
Sampling period | 115418000 Milliseconds
Power reading state | Activated
```

### GetAssetTag
```
Asset Tag: AssetTag_example
```

### GetCap (NM20)
```
Enhanced Power Statistics attributes
DCMI Version :1.1
Parameter Revision:2
The number of supported rolling average time periods:9
Rolling Average Time periods:
 05 - 5 Seconds
 0F - 15 Seconds
 1E - 30 Seconds
 41 - 1 Minutes
 43 - 3 Minutes
 47 - 7 Minutes
 4F - 15 Minutes
 5E - 30 Minutes
 81 - 1 Hours
```

### GetPowerReading (NM20)
```
Instantaneous power reading | 107 W
Minimum during sampling period | 77 W
Maximum during sampling period | 207 W
Average during sampling period | 126 W
IPMI timestamp | 2023/08/28 07:54:00
Sampling period | 5 Seconds
Power reading state | Activated
```

### GetPowerLimit (NM20)
```
Exception actions :Hard power off system and log event to SEL
Power limit requested :200 W
Correction time limit :20000 ms
Management application statistics sampling period :50 s
```

## Notes

- Starting with Intel's 14th generation platforms, only the following `--action` values with `--type STD_DCMI` are supported: `SetMCID`, `GetMCID`, `GetPowerStatus`, `SetAssetTag`, and `GetAssetTag`. Other actions and `--type NM20` options are not supported on these platforms because they lack the Management Engine (ME) required for Intel Node Manager functionality.
- For `GetPowerReading`, use `DcmiManage --type NM20 --action GetCap` first to get the supported rolling average time periods (hex values) for use with `--period`.
- The execution progress for the managed system is continuously updated in the Execution Message section of the created log file.
