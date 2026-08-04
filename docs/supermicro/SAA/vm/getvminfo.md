# GetVmInfo

Gets virtual media information from the managed system. Supported on platforms with a single virtual media device as well as platforms that support multiple virtual media devices.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetVmInfo [--dev_id <device ID>]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c GetVmInfo [--dev_id <device ID>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetVmInfo [--dev_id <device ID>]
```

## Options

- `--dev_id <Device ID>` (Optional): Uses the specified device ID to get virtual media information. The supported device ID: [1-3].

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetVmInfo
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetVmInfo --dev_id 1
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetVmInfo
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetVmInfo --dev_id 1
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetVmInfo --dev_id 1
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

### Single Virtual Media Device Platform
```
SuperServer Automation Assistant 1.0.0 (2023/11/28) (x86_64)
Copyright(C) 2023 Super Micro Computer, Inc. All rights reserved.
Status: Start to get virtual media information.
Managed system................192.168.34.56
 Virtual media status......Enable
 Virtual media port........623
Virtual Media Device Information
=============================
 Device 1
 ============
 Device status: Unmounted
 Media type: N/A
 Connection setting: NotConnected
 Image: N/A
 SSL certificate verified: N/A
 Self-signed certificate accepted: N/A
 UserName: N/A
 Device 2
 ============
 Device status: Unmounted
 Media type: N/A
 Connection setting: NotConnected
 Image: N/A
 SSL certificate verified: N/A
 Self-signed certificate accepted: N/A
 UserName: N/A
 Device 3
 ============
 Device status: Unmounted
 Media type: N/A
 Connection setting: NotConnected
 Image: N/A
 SSL certificate verified: N/A
 Self-signed certificate accepted: N/A
 UserName: N/A
```

### Multiple Virtual Media Device Platform (Empty Devices)
```
Managed system................192.168.34.56
 Virtual media status......Enable
 Virtual media port........623
Virtual Media Device Information
=============================
 Device 1: Empty device
 Device 2: Empty device
 Device 3: Empty device
```

### Multiple Virtual Media Device Platform (Mounted by iKVM)
```
Managed system................192.168.34.56
 Virtual media status......Enable
 Virtual media port........623
Virtual Media Device Information
=============================
 Device 1
 ============
 Device status: Mounted
 Media type: Floppy
 Connection setting: Applet
 Image: kvm_floppy
```

## Notes

- If the execution "Status" field for a managed system is SUCCESS, the console output of the managed system will be shown in the Execution Message section of the created log file.
- If a device is mounted by iKVM, it can only be unmounted by iKVM.
