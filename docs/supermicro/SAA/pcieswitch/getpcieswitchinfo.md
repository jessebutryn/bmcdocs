# GetPCIeSwitchInfo

Gets and reads the PCIe Switch information from the managed system, and parses PCIe Switch information from a firmware image file.

## Syntax

### Single System

#### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetPCIeSwitchInfo
```

#### In-Band
```
saa -c GetPCIeSwitchInfo [--file <filename> [--file_only]]
```

### Multiple Systems

#### OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetPCIeSwitchInfo
```

## Options

- `--file <file name>` (Optional): Reads the PCIe Switch information from an input PCIe Switch image file.
- `--showall` (Optional): Shows additional information about the PCIe Switch device.
- `--file_only` (Optional): Works with the `--file` option, and only reads PCIe Switch information from the input image file.

## Examples

### In-Band
```bash
[SAA_HOME]# ./saa -c GetPCIeSwitchInfo
```

```bash
[SAA_HOME]# ./saa -c GetPCIeSwitchInfo --file fw_file.img --file_only
```

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetPCIeSwitchInfo
```

## Output

### Broadcom Chipset (H12DGQ-NT6)
```
Managed system..........................localhost
PCIe Switch Device Vendor............... Broadcom
 Device ID(0)
 Device Name.........................SwitchPlx0
 Pex Cfg Version.....................1209
 Device ID(1)
 Device Name.........................SwitchPlx1
 Pex Cfg Version.....................1209
 Device ID(2)
 Device Name.........................SwitchPlx2
 Pex Cfg Version.....................3407
 Device ID(3)
 Device Name.........................SwitchPlx3
 Pex Cfg Version.....................3407
Local Firmware File.................... H12DGQ_NT6_1207_PWR.bin
PCIe Switch Device Vendor...............Broadcom
 Pex Cfg Version.....................1207
```

### Microchip Chipset (X12DSC-6 with AOM-S3616-S/AOM-SADPT-S)
```
Managed system..........................localhost
PCIe Switch Device Vendor...............Microchip
 Device ID(0)
 Device Name.....................switchtec0
 FW Version......................3.60 B049
 CFG CRC.........................d9bd7434
Local Firmware File....................MCH036B360049_20201210.fwimg
PCIe Switch Device Vendor...............Microchip
 Generation..........................GEN4
 Type................................CFG
 Version.............................3.60 B049
 Image Length........................267768 bytes
 CRC.................................101a194c
 Secure Version......................00000000
```

### Broadcom Chipset, Synthetic Mode (X13DEG-PVC)
```
Managed system..........................localhost
 Device ID(0)
 Device Name.....................SwitchPlx0
 Chip Vendor.....................Broadcom
 Work Mode.......................Base Mode
 Generation......................5
 Subsystem ID....................0072
 SBR version.....................00161176
 Device ID(1)
 Device Name.....................SwitchPlx1
 Chip Vendor.....................Broadcom
 Work Mode.......................Base Mode
 Generation......................5
 Subsystem ID....................0072
 SBR version.....................00173F18
 Device ID(2)
 Device Name.....................SwitchPlx2
 Chip Vendor.....................Broadcom
 Work Mode.......................Synthetic Mode
 Generation......................5
 FW version......................04:11:00:00
 SBR version.....................00:23:24:82
 MfgRevision.....................00:23:24:82
 Platform Name...................AOM-SXM5-IO
 Device ID(3)
 Device Name.....................SwitchPlx3
 Chip Vendor.....................Broadcom
 Work Mode.......................Synthetic Mode
 Generation......................5
 FW version......................04:11:00:00
 SBR version.....................00:23:24:82
 MfgRevision.....................00:23:24:82
 Platform Name...................AOM-SXM5-IO
```

## Notes

- This command is available on the H12DGQ-NT6 with Broadcom PCIe Switch Gen4 Series chipsets, X13DEG-PVC with Broadcom PCIe Switch Gen5 Series chipsets, and X12DSC-6 with Microchip PCIe Switch Gen4 Series chipsets platforms.
- On the H12DGQ-NT6 and X13DEG-PVC platforms with Broadcom PCIe Switch chipsets, find the readme.txt in the `SAA/driver/broadcom/PlxSdk` folder to load the device driver.
- On the X12DSC-6 platform with Microchip PCIe Switch Gen4 Series chipsets, download the SDK from Microsemi and follow the instructions on the website to load the device driver.
- Supported Operating System: Ubuntu 20.04 and later. The build device driver environment must have installed packages such as cmake and gcc.
