# UpdateGpu

## Description

Use the "UpdateGpu" command with the CEC/FPGA/HGX_H100/H100_FPGA/Intel_Gaudi2/Intel PVC of GPU firmware image to update the GPU firmware of a managed system by SUM.

## Syntax

### Single System

#### OOB
```
sum -i <IP or host name> -u <username> -p <password> -c UpdateGpu --item <CEC|FPGA|HGX_H100|H100_FPGA|PVC_RETIMER|GAUDI_RETIMER|PVC_AMC|PVC_UBB_CPLD|MGX_GPU> --file <filename> [--reboot] [--post_complete] [--dev_id <device ID>]
```

#### In-Band
```
sum -I Redfish_HI -u <username> -p <password> -c UpdateGpu --item <CEC|FPGA|HGX_H100|H100_FPGA|PVC_RETIMER|GAUDI_RETIMER|PVC_AMC|GAUDI_UBB_CPLD> --file <filename> [--reboot] [--post_complete] [--dev_id <device ID>]
```

```
sum -c UpdateGpu --dev_id <device_id> --item <GAUDI_OAM_CPLD|GAUDI_SPI|PVC_IFWI|PVC_PSCBIN> --file <filename> [--reboot] [--dev_id <device ID>]
```

#### Remote In-Band
```
sum -I Remote_INB --oi <IP address> --ou <username> --op <password> -c UpdateGpu --dev_id <device_id> --item <GAUDI_OAM_CPLD|GAUDI_UBB_CPLD|GAUDI_SPI|PVC_IFWI|PVC_PSCBIN> --file <filename> [--reboot] --remote_sum <remote sum_location> [--dev_id <device ID>]
```

### Multiple Systems

#### OOB
```
sum -l <system list file> [-u <username> -p <password>] -c UpdateGpu --item <CEC|FPGA|HGX_H100|H100_FPGA|PVC_RETIMER|GAUDI_RETIMER|PVC_AMC|PVC_UBB_CPLD|MGX_GPU> --file <filename> [--reboot] [--post_complete] [--dev_id <device ID>]
```

#### Remote In-Band
```
sum -I Remote_INB -l <system list file> -c UpdateGpu --dev_id <device_id> --item <GAUDI_OAM_CPLD|GAUDI_UBB_CPLD|PVC_IFWI|PVC_PSCBIN|GAUDI_SPI> --file <filename> [--reboot] --remote_sum <remote sum_location> [--dev_id <device ID>]
```

## Options

- `--item <item_type>`: Specifies the GPU component to update (e.g., CEC, FPGA, HGX_H100, etc.).
- `--file <filename>`: Specifies the GPU firmware image file.
- `--reboot`: Reboots the system after update.
- `--post_complete`: Waits for POST to complete after reboot.
- `--dev_id <device ID>`: Specifies the device ID.
- `--remote_sum <remote sum_location>`: Specifies the path to remote SUM executable.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateGpu --file GPU_CEC.bin --item CEC
```

The console output contains the following information.

```
Managed system................192.168.34.56
 HGX Model................HGX A100
 CEC version................4.0
 FPGA version................3.03
Local GPU CEC image file......GPU_CEC.bin
Status: Start updating CEC for 192.168.34.56
************************************WARNING****************************
 Do not remove AC power from the server.
************************************************************************
Uploading GPU CEC FW...Done
Updating GPU CEC FW ...>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>Done
Status: GPU CEC is updated for 192.168.34.56
Note: You have to reboot or power up the system for the changes to take effect
```

```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateGpu --file NVDIA_HGX_H100.pkg --item HGX_H100 --reboot --post_complete
```

## Notes

- The UpdateGpu command only supports NVIDIA GPU.
- Supported platforms vary by GPU type and chipset.
