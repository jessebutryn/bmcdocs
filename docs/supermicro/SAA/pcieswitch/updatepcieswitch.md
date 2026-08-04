# UpdatePCIeSwitch

Updates the PCIe Switch firmware of a managed system using a PCIe Switch firmware image.

## Syntax

### Single System

#### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdatePCIeSwitch {--dev_id <index>} {--file <filename>}
```

#### In-Band
```
saa -c UpdatePCIeSwitch {--dev_id <index>} {--file <filename>}
```

## Options

- `--file <file name>` (Optional): PCIe switch firmware file.
- `--dev_id <Device ID>`: PCIe switch device ID. Can be retrieved with the `GetPCIeSwitchInfo` command.
- `--reboot` (Optional): Forces the managed system to power cycle after operation.

## Examples

### In-Band
```bash
[SAA_HOME]# ./saa -c UpdatePCIeSwitch --file fw_file.img --dev_id 0
```

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdatePCIeSwitch --file fw_file.fw --dev_id 0
```

## Output

### Broadcom Chipset (H12DGQ-NT6)
```
Managed system..........................localhost
PCIe Switch Device Vendor...............Broadcom
 Device ID(0)
 Device Name.........................SwitchPlx0
 Pex Cfg Version.....................1207
Local Firmware File......................H12DGQ_NT6_1209_PWR.bin
PCIe Switch Device Vendor................Broadcom
 Pex Cfg Version......................1209
Update firmware progress Started ...
Writing Firmware ........................(100%)
Update firmware progress Finished.
Update firmware success.
```

### Microchip Chipset (X12DSC-6 with AOM-S3616-S/AOM-SADPT-S)
```
Managed system..........................localhost
PCIe Switch Device Vendor...............Microchip
 Device ID(0)
 Device Name.........................switchtec0
 FW Version..........................3.60 B049
 CFG CRC.............................101a194c
Local Firmware File.....................MCH036B360049_20201210.fwimg
PCIe Switch Device Vendor...............Microchip
 Generation..........................GEN4
 Type................................CFG
 Version.............................3.60 B049
 Image Length........................267768 bytes
 CRC.................................101a194c
 Secure Version......................00000000
Update firmware progress Started ...
Writing Firmware ....................... (100%)
Update firmware progress Finished.
```

### Broadcom Chipset, Base Mode (X13DEG-PVC)
```
Update firmware success.
Note: Please reboot the system to activate the updated image
Managed system..........................localhost
 Device ID(0)
 Device Name.....................SwitchPlx0
 Chip Vendor.....................Broadcom
 Work Mode.......................Base Mode
 Generation......................5
 Subsystem ID....................0072
 SBR version.....................00161176
Local Firmware File.................AOM_DP801_SW_bSW_SHP.sbr.FwTableTmp.hash.signed.bin
 Chip Vendor.....................Broadcom
 Work Mode.......................Base Mode
 Generation......................5
 SBR Version.....................0016BAB0
Update firmware progress Started ...
Writing Firmware ....................... (100%)
Update firmware progress Finished.
Update firmware success.
Note: Please do power cycle to activate the updated image.
```

## Notes

- This command is available on the H12DGQ-NT6 with Broadcom PCIe Switch Gen4 Series chipsets, X13DEG-PVC with Broadcom PCIe Switch Gen5 Series chipsets, and X12DSC-6 with Microchip PCIe Switch Gen4 Series chipsets platforms.
- On the H12DGQ-NT6 and X13DEG-PVC platforms with Broadcom PCIe Switch chipsets, find the readme.txt in the `SAA/driver/broadcom/PlxSdk` folder to load the device driver.
- On the X12DSC-6 platform with Microchip PCIe Switch Gen4 Series chipsets, download the SDK from Microsemi and follow the instructions on the website to load the device driver.
- Supported Operating System: Ubuntu 20.04 and later. The build device driver environment must have installed packages such as cmake and gcc.
- After updating, either reboot (base mode) or power cycle (synthetic mode) the system to activate the updated image, per the console output.
