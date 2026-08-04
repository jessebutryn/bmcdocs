# GetNvmeInfo

Gets the current NVMe device information from the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetNvmeInfo [--dev_id <device_id>] [--redfish]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetNvmeInfo [--dev_id <device_id>]
saa -c GetNvmeInfo [--dev_id <device_id>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetNvmeInfo [--dev_id <device_id>]
```

## Options

- `--dev_id <Device ID>`: NVMe device controller ID. Prints all NVMe information on the screen if the file-saving function is not available (optional).
- `--redfish`: Enables support for pure Redfish (optional).

## Examples

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetNvmeInfo --dev_id 0
```

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.3.4 -u ADMIN -p PASSWORD -c GetNvmeInfo --dev_id 0
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetNvmeInfo
```

## Output

### Via Redfish (In-Band)
```
NVMe Device information
=======================
 [NVMe Controller(1)]
 [Group(1)]
 Group ID: 0
 [NVMe SSD(1)]
 Name: Disk.Bay.1
 Manufacturer: Samsung
 Model Number: SAMSUNG MZ3LO1T9HCJR-00A07
 Serial Number: S79JNG0X102271
 Capacity Bytes: 1920383410176
 Capable SpeedGbs: 126.000000
 Percecntage Drive Life Used: 0
 Drive Functional: true
 Temperature: 26 degree C
 Failure Predicted: false
 Status Indicator: OK
```

### Via TAS (OOB)
```
NVMe Device information
=======================
 [NVMe Controller(1)]
 Device ID: 0
 [Group(1)]
 Group ID: 0
 [NVMe SSD(1)]
 Name: vmhba1
 Slot: 0
 Temperature: 51 degree C
 Capacity: 1000 GB
 Temperature: 37 degree C
 Device Class: Mass storage controller
 Device SubClass: Non-Volatile memory controller
 Device Program Interface: NVM express
 Vendor Name: Samsung Electronics Co., Ltd.
 Serial Number: S1NONYAF800079
 Model Number: MZWEI400HAGM-0003
 Port 0 Max Link Speed: 8 GT/s
 Port 0 Max Link Width: x4
 Port 1 Max Link Speed: N/A
 Port 1 Max Link Width: N/A
 Initial Power Requirement: 10 Watts
 Max Power Requirement: 25 Watts
 Located Status: Not Located
```

### TAS Not Installed
If TAS is not installed on the machine, fields that require it (such as Name and Capacity) display "Please install TAS" instead of a value.

## Notes

- If the execution Status field of the managed system shows SUCCESS, the console output of the managed system will be shown in the Execution Message section of the created log file.
