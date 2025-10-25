# GetGpuInfo

## Description

Use the "GetGpuInfo" command to get the current GPU information from the managed system.

## Syntax

### Single System

#### OOB
```
sum -i <IP or host name> -u <username> -p <password> -c GetGpuInfo [--show_all] [--showoam <oam id>] [--file <filename>]
```

#### In-Band
```
sum [-I Redfish_HI -u <username> -p <password>] -c GetGpuInfo [--show_all] [--showoam <oam id>]
```

#### In-Band (for Intel Gaudi2)
```
sum -c GetGpuInfo [--show_all] [--file <filename>] [--showoam <oam id>]
```

#### Remote In-Band
```
sum -I Remote_INB --oi <IP address> --ou <username> --op <password> -c GetGpuInfo [--show_all] [--showoam <oam id>] [--file <filename>]
```

### Multiple Systems

#### OOB
```
sum -l <system list file> [-u <username> -p <password>] -c GetGpuInfo [--showoam <oam id>] [--file <filename>]
```

#### Remote In-Band
```
sum -I Remote_INB -l <system list file> -c GetGpuInfo [--show_all] [--showoam <oam id>] [--file <filename>]
```

## Options

- `--show_all`: Shows all GPU information.
- `--showoam <oam id>`: Shows OAM information for the specified OAM ID.
- `--file <filename>`: Saves the GPU information to the specified file.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetGpuInfo
```

### In-Band
```
[SUM_HOME]# ./sum -c GetGpuInfo
```

```
[SUM_HOME]# ./sum -I Redfish_HI -u ADMIN -p PASSWORD -c GetGpuInfo
```

The console output contains the following information of the managed system with add-on GPU cards installed.

```
GPU information
===================
[GPU(1)]
 Brand : NVIDIA
 Location : 2
 Model : Tesla P100-PCIE-12GB
 Serial Number : 0325117155632
 Part Number : 15F7-893-A1
 Firmware Version : 86.00.4D.00.03
 GPU GUID : df5f42692dc92dc40e301b746505f5ae
 Board Part Number : 900-2H400-0010-000
 InfoROM Version : H400.0202.00.01
 Memory Vendor : S
 Temperature(C) : 1 degreeC
```

The console output contains the following information for HGX system on X12/H12 systems.

```
HGX information
===================
CEC Version....................3.9
FPGA Version...................2.A5
[GPU(1)]
 Brand : NVIDIA
 Location : 0
 Model : NVIDIA A100-SXM4-80GB
 Part Number : 20B2-895-A1
 Firmware Version : 92.00.45.00.05
 GPU GUID : 74f76243ff58e56784bed8928ff4ff71
 InfoROM Version : G506.0210.00.03
 Temperature(C) : 32 degreeC
[GPU(2)]
 Brand : NVIDIA
 Location : 0
 Model : NVIDIA A100-SXM4-80GB
 Part Number : 20B2-895-A1
 Firmware Version : 92.00.45.00.05
 GPU GUID : fbec45bdd281d823c9b30edf38379387
 InfoROM Version : G506.0210.00.03
 Temperature(C) : 29 degreeC
[GPU(3)]
 Brand : NVIDIA
 Location : 0
 Model : NVIDIA A100-SXM4-80GB
 Part Number : 20B2-895-A1
 Firmware Version : 92.00.45.00.05
 GPU GUID : e34eb0db342be31e5e15855f2e91a00b
 InfoROM Version : G506.0210.00.03
 Temperature(C) : 30 degreeC
```

## Notes

- The GetGpuInfo command only supports NVIDIA GPU.
