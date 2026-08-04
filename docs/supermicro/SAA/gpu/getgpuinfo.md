# GetGpuInfo

Gets the current GPU information from the managed system, including add-on GPU cards, HGX baseboard GPUs, MGX/GB200 GPUs, and Intel Gaudi2/Gaudi3 GPU cards.

## Syntax

### Single System

#### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetGpuInfo [--show_all] [--showoam <oam id>] [--file <filename>]
```

#### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c GetGpuInfo [--show_all] [--showoam <oam id>]
```

#### In-Band (Intel Gaudi2/3)
```
saa -c GetGpuInfo [--show_all] [--file <filename>] [--showoam <oam id>]
```

#### Remote In-Band
```
saa -I Remote_INB --oi <OS IP address> --ou <OS username> --op <OS password> -c GetGpuInfo [--show_all] [--showoam <oam id>] [--file <filename>] [--remote_saa <remote SAA path>]
```

### Multiple Systems

#### OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetGpuInfo [--showoam <oam id>] [--file <filename>]
```

#### Remote In-Band
```
saa -I Redfish_HI -l <system list file> -c GetGpuInfo [--show_all] [--showoam <oam id>] [--file <filename>] [--remote_saa <remote SAA path>]
```

## Options

- `--showall`: Prints the FRU information on the GPU baseboard of the managed system. Only supported on X11/H11 with HGX2 system and Intel Gaudi 2/3 system.
- `--showoam <oam id>` (Optional): For Intel PVC and Intel Gaudi2 systems, shows individual OAM information.
- `--file <file name>` (Optional): Reads the GPU information from an input GPU image file.
- `--file_only` (Optional): Works with `--file`, and only reads GPU information from the input image file.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetGpuInfo
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetGpuInfo
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetGpuInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetGpuInfo
```

## Output

### Add-on GPU Cards
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

### HGX System (X12/H12, NVIDIA A100)
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
[HGX Delta System Temperature]
[HBM]
 Reading Temperature : 36 degreeC
 HBM 1 Temperature : 36 degreeC
 HBM 2 Temperature : 33 degreeC
[NVLink Switch]
 Reading Temperature : 31 degreeC
 NVLink SW 1 Temperature : 30 degreeC
[PCI Switch]
 Reading Temperature : 57 degreeC
 PCI SW 1 Temperature : 24 degreeC
[GPU Board]
 Reading Temperature : 36 degreeC
 GPU Board 1 Temperature : 36 degreeC
[PLX]
 Reading Temperature : 68 degreeC
 PLX 1 Temperature : 63 degreeC
[Pump]
 Pump Temperature : 0 degreeC
```

### HGX H100 System (X13/H13)
```
Managed system.................192.168.34.56
 HGX Model..................HGX H100 8-GPU
 HMC
 version................HGX-22.10-1-rc31
 ERoT version...........00.02.0120.0000_n00
 FPGA
 version................2.0E
 ERoT version...........00.02.0120.0000_n00
 PCIe Switch
 version................1.7.5F
 ERoT version...........00.02.0120.0000_n00
 GPU SXM [1]
 version................96.00.61.00.01
 ERoT version...........00.02.0120.0000_n00
 NVSwitch [0]
 version................96.10.35.00.01
 ERoT version...........00.02.0120.0000_n00
 PCIe Retimer [0]
 version................1.31.X
HGX information
===================
[UBB (1)]
 Name : GPU Baseboard
 Model : HGX_H100
 Manufacturer : NVIDIA
 Serial Number : 1664922651034
 Part Number : 935-24287-0000-000
 Chassis Type : Zone
[GPU(1)]
 Location : 1
 Model : H100 80GB HBM3
 Serial Number : 1655022001438
 Part Number : 2330-885-A1
 Firmware Version : 96.00.46.00.0E
 Temperature(C) : 43 degreeC
```

### MGX/GB200 System
```
[GPU 4]
 Name : HGX_GPU_3
 Model : GB200
 Manufacturer : NVIDIA
 Serial Number : 1654024000895
 Part Number : 690-2G548-0201-QS1
 PowerState : On
 MaxPowerWatts : 1200 watts
 MinPowerWatts : 200 watts
 LocationType : Embedded
 Temperature(C) : 33 degreeC.
 Temperature1(C) #Headroom : 58.09 degreeC.
 InterfaceType : PCIe
 LanesInUse : 1
 MaxLanes : 16
 MaxPCIeType : Gen5
 PCIeType : Gen4
[GPU IRot1]
 Name : HGX_IRoT_GPU_0
 Manufacturer : NVIDIA
 Serial Number : 0xDF88A2EBEC584E5B
 LocationType : Embedded
```

### Intel Gaudi2 System
```
Managed system..........................localhost
 Habana UBB CPLD version.............000A0A02
 Habana OAM CPLD version
 Device Id(0)
 Version.....................0F
 Configration ID.............01
 SPI Firmware Version:
 Device ID.......................b3:00.0
 OAM ID......................0
 Serial Number...............AM27043716
 Module ID...................6
 Firmware [SPI] Version......Preboot version hl-gaudi2-1.10.0-fw43.2.0-sec-4 (May 17 2023 - 20:08:22)
```

### Intel Gaudi3 System
```
Managed system..........................localhost
 Device ID...........................17:00.0
 Product Name....................HL-325L
 Model Number....................F08GL0DIG017A
 Serial Number...................AO40020264
 Module ID.......................0
 Firmware [SPI] Version..........Preboot version hl-gaudi3-1.20.0-fw58.1.1-sec-2 (Feb 13 2025 - 12:01:58)
 Firmware [OS] Version...........Zephyr 2.7.2-hl-gaudi3-1.20.0-fw-58.1.1-sec-2 (Feb 13 2025 - 12:00:59)
 OAM CPLD Version................Version: 0x4, Timestamp(epoch): 0x67b607ae [Wed Feb 19 08:32:46 2025]
 OAM Device Type.................15D-HBN/15-HBN-MP
 OAM Key Type....................1
 PCB Assembly Version............V0P
 PCB Version.....................R01
 HL Revision.....................1
 AIP UUID........................01P4-0A0903LH-18-U4V193-04-04-05
```

## Notes

- If the "Status" field of a managed system is SUCCESS, the GPU information of the managed system will be shown in the "Execution Message" section of the managed system in the created log file (multiple systems OOB usage).
- For a comprehensive list of supported platforms and product SKUs, refer to the "GetGpuInfo/UpdateGpu supported platform matrix" appendix in the SAA User's Guide.
