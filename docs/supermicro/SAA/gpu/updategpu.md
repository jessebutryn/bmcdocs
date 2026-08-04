# UpdateGpu

Updates the GPU firmware of a managed system using a GPU firmware image that matches the FW item type — for example CEC, FPGA, HGX, HGX_GPU, PVC_RETIMER, Intel_Gaudi2/3 components, MGX_GPU, MI300X, and related ERoT/CPLD/retimer images.

## Syntax

### Single System

#### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UpdateGpu --item <CEC|FPGA|HGX|HGX_FPGA|HGX_FPGA_EROT|HGX_HMC|HGX_HMC_EROT|HGX_PCIESWITCH|HGX_PCIESWITCH_EROT|HGX_GPU|HGX_GPU_EROT|HGX_NVSWITCH|HGX_NVSWITCH_EROT|HGX_RETIMER|PVC_RETIMER|GAUDI_RETIMER|PVC_AMC|PVC_UBB_CPLD|MGX_GPU|MI300X|ONBOARD_RETIMER|HGX_NVLINKMANAGEMENTNIC|HGX_NVLINKMANAGEMENTNIC_EROT|GAUDI_UBB_CPLD|GAUDI_UBB_CPLD2> --file <filename> [--reboot] [--post_complete] [--dev_id <device ID>]
```

#### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c UpdateGpu --item <CEC|FPGA|HGX|HGX_FPGA|HGX_FPGA_EROT|HGX_HMC|HGX_HMC_EROT|HGX_PCIESWITCH|HGX_PCIESWITCH_EROT|HGX_GPU|HGX_GPU_EROT|HGX_NVSWITCH|HGX_NVSWITCH_EROT|HGX_RETIMER|PVC_RETIMER|GAUDI_RETIMER|PVC_AMC|GAUDI_UBB_CPLD|MI300X|ONBOARD_RETIMER|HGX_NVLINKMANAGEMENTNIC|HGX_NVLINKMANAGEMENTNIC_EROT> --file <filename> [--reboot] [--dev_id <device ID>]
```

For Intel Gaudi2:
```
saa -c UpdateGpu --dev_id <device_id> --item <GAUDI_OAM_CPLD|GAUDI_SPI|PVC_IFWI|PVC_PSCBIN> --file <filename> [--reboot] [--dev_id <device ID>]
```

For Intel Gaudi3:
```
saa -c UpdateGpu --item <GAUDI_OAM_CPLD|GAUDI_SPI> --file <filename> [--reboot]
```

#### Remote In-Band
```
saa -I Remote_INB --oi <IP address> --ou <username> --op <password> -c UpdateGpu {--item <GAUDI_OAM_CPLD|GAUDI_UBB_CPLD|GAUDI_SPI|PVC_IFWI|PVC_PSCBIN> --file <filename>} [--reboot] [--remote_saa <remote saa_location>] [--dev_id <device ID>]
```

### Multiple Systems

#### OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UpdateGpu {--item <CEC|FPGA|HGX|HGX_FPGA|PVC_RETIMER|GAUDI_RETIMER|PVC_AMC|PVC_UBB_CPLD|MGX_GPU|MI300X|HGX_RETIMER|ONBOARD_RETIMER|GAUDI_UBB_CPLD|GAUDI_UBB_CPLD2> --file <filename>} [--reboot [--post_complete]] [--dev_id <device ID>]
```

#### Remote In-Band
```
saa -I Redfish_HI -l <system list file> -c UpdateGpu {--item <GAUDI_OAM_CPLD|GAUDI_UBB_CPLD|PVC_IFWI|PVC_PSCBIN|GAUDI_SPI> --file <filename>} [--reboot] [--remote_saa <remote saa_location>] [--dev_id <device ID>]
```

## Options

- `--item <item name>`: FW item type of GPU firmware. Values: `1 = CEC`, `2 = FPGA`, `3 = HGX`, `4 = PVC_IFWI`, `5 = PVC_PSCBIN`, `6 = PVC_UBB_CPLD`, `7 = PVC_RETIMER`, `8 = PVC_AMC`, `9 = GAUDI_SPI`, `10 = GAUDI_OAM_CPLD`, `11 = GAUDI_RETIMER`, `12 = GAUDI_UBB_CPLD`, `13 = GAUDI_UBB_CPLD2`, `14 = HGX_FPGA`, `15 = HGX_HMC`, `16 = HGX_HMC_EROT`, `17 = HGX_FPGA_EROT`, `18 = HGX_PCIESWITCH`, `19 = HGX_PCIESWITCH_EROT`, `20 = HGX_GPU`, `21 = HGX_GPU_EROT`, `22 = HGX_NVSWITCH`, `23 = HGX_NVSWITCH_EROT`, `24 = HGX_RETIMER`, `25 = MGX_GPU`, `26 = MI300X`, `27 = ONBOARD_RETIMER`, `28 = HGX_NVLINKMANAGEMENTNIC`, `29 = HGX_NVLINKMANAGEMENTNIC_EROT`, `30 = HGX_GPU_INFOROM`, `31 = HGX_CPLD`, `32 = HGX_CPU`, `33 = HGX_CPU_EROT`.
- `--file <file name>`: Updates the GPU firmware file that matches the FW item type.
- `--dev_id <Device ID>` (Optional): Retrieved with the `GetGpuInfo` command. For SPI-FW, use the device address. For HGX Retimer, HGX GPU, HGX GPU ERoT, HGX NVSwitch, and HGX NVSwitch ERoT, use the device ID.
- `--reboot` (Optional): Forces the managed system to reboot or power up after operation.
- `--post_complete` (Optional): Waits for the managed system's POST to complete after reboot.
- `--remote_saa <remote saa_location>`: Path to the remote SAA executable (for remote in-band usage).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateGpu --file GPU_CEC.bin --item CEC
```

```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateGpu --file NVDIA_HGX_H100.pkg --item HGX --reboot --post_complete
```

```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p QHKPSPALGW -c UpdateGpu --item PVC_Retimer --dev_id 3 --file pt516_x16_reversed_v2_7_0.bin
```

```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateGpu --file MI300X.pldm --item MI300X --reboot
```

```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdateGpu --item onboard_retimer --file pt516_x16_reversed_v2_7_0.bin
```

```bash
[SAA_HOME]# ./saa -i 10.141.176.170 -u ADMIN -p ADMIN -c UpdateGpu --item gaudi_retimer --dev_id 1 --file UBB_2.8.45_Retimer.ihx
```

```bash
[SAA_HOME]# ./saa -i 10.141.176.170 -u ADMIN -p ADMIN -c UpdateGpu --item gaudi_ubb_cpld --file HLB-325_Primary_R0A_20240611a_FPGA_00_0c_RevD.svf
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateGpu --file GPU_FPGA.bin --item FPGA

[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c UpdateGpu --file NVDIA_HGX_H100.pkg --item HGX --reboot

[SAA_HOME]# ./saa -c UpdateGpu --dev_id 1 --file HL225_PFR_20230427_0F_644A7EDA_production.signed_cfg0.svf --item GAUDI_OAM_CPLD

[SAA_HOME]# ./saa -c UpdateGpu --item GAUDI_OAM_CPLD --file gaudi3-cpldLFMXO5-15D-03-TS66530567.itb

[SAA_HOME]# ./saa -c UpdateGpu --item PVC_UBB_CPLD --file Etron_UBBSA_CPLD1_A02.jed --dev_id 0

[SAA_HOME]# ./saa -c UpdateGpu --item gaudi_spi --file habanalabs-firmwareodm-1.10.0-494.amd64.deb --dev_id cc:00.0

[SAA_HOME]# ./saa -c UpdateGpu --item gaudi_spi --file habanalabs-firmwareodm-1.17.0-343.amd64.deb
```

### Remote In-Band
```bash
saa -I Remote_INB -oi 1.1.1.1 -ou root -op 1234 -c UpdateGpu --dev_id 0 --item PVC_UBB_CPLD --file Etron_UBB-SA_CPLD1_A02.jed --remote_saa root/saa
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UpdateGpu --item FPGA --file GPU_FPGA.bin
```

### Multiple Systems Remote In-Band
```bash
saa -I Remote_INB -l SList.txt -c UpdateGpu --dev_id 0 --item PVC_UBB_CPLD --file Etron_UBB-SA_CPLD1_A02.jed --remote_saa root/saa

[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c UpdateGpu --item gaudi_spi --file habanalabs-firmware-odm-1.10.0-494.amd64.deb --dev_id cc:00.0
```

`SList.txt` for remote in-band usage takes the form:
```
1.1.1.1 root 1234
1.1.1.2 root 4321
```

## Output

### CEC Update
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

### HGX H100 Update with Reboot and Post-Complete
```
Managed system.................192.168.34.56
 HGX Model..................HGX H100 8-GPU
 HMC
 version................HGX-22.10-1-rc31
 ERoT version...........00.02.0120.0000_n00
Local GPU image file.........../home/user/GPU/nvfw_HGXH100x8_0002_221216.1.0_prod-signed.fwpkg
Status: Start updating HGX for 192.168.34.56
Uploading HGX FW...............................Done
Updating HGX FW...>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>Done
Status: HGX is updated for 192.168.34.56
Status: The managed system 192.168.34.56 is rebooting.
Status: The managed system 192.168.34.56 is waiting for POST complete
Status: MemoryInitializationStarted
Status: PCIResourceConfigStarted
Status: The managed system 192.168.34.56 is POST completed
```

### AMD MI300X Update
```
Managed system................. 192.168.34.68
Model..........................AMD Instinct MI300X UBB
 SMC
 version................t28_v2.11.0.32
 SMC FPGA
 version................T28_S_v0.0C.0.73803c2d
 UBB Bundle
 version................BKC_X23.44.09.76
 GPU IFWI
 version................vBRP018G_85284
 Retimers
 version................v2_8_76
 OAM RM
 version................v4_0_9
 ROT
 version................aa04
 UBB FPGA
 version................v0.21.2.a657321d
Local GPU MI300X image file.............MI300X.pldm
 GPU MI300X image file version.......BKC_X23.44.09
Status: Start updating MI300X for 192.168.34.68
Uploading MI300X FW......................Done
Updating MI300X FW...>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>Done
Status: The managed system 192.168.34.56 is rebooting.
WARNING: Without option --post_complete, please manually confirm the managed system is POST complete before executing next action.
```

### Gaudi3 UBB CPLD Update
```
Managed system.................10.141.176.170
Gaudi UBB CPLD Version.........00.0C
Gaudi UBB CPLD image file......HLB-325_Primary_R0A_20240611a_FPGA_00_0c_RevD.svf
Status: Start updating Gaudi 3 UBB CPLD for 10.141.176.170
Uploading Gaudi 3 UBB CPLD FW.......
Updating Gaudi 3 UBB CPLD FW...>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>Done
Status: Gaudi 3 UBB CPLD is updated for 10.141.176.170
```

## Notes

- It is only used for updating NVIDIA HGX A100 8-GPU (Delta), NVIDIA HGX H100/H200 8-GPU (Delta Next), Intel PVC, Intel Gaudi2/3, CG1 MGX, and AMD MI300X system firmware. For a comprehensive list of supported platforms and product SKUs, refer to the "GetGpuInfo/UpdateGpu supported platform matrix" appendix.
- On the Intel PVC system, `igsc` must be installed to communicate with the PVC_IFWI and PVC_PSCBIN devices.
- On the Intel Gaudi2/3 system, Habana libraries (`hl-fw-loader` and `hl-smi`) with Ubuntu 20.04 are required.
- On the Intel Gaudi2 system, an additional add-on package (`AddOn_GD2_Linux_x86_64_YYYYMMDD.tar.gz`) should be extracted in the `tool` directory under the SAA installed path; contact Supermicro for assistance downloading the add-on package.
- On the Intel Gaudi2/3 system, a power cycle must be performed for the Habana driver's `hl-smi` and `hl-fw-loader` before updating the `gaudi_spi` firmware.
- In the device_id for `gaudi_spi` on the Intel Gaudi2 system, it should be a device address (e.g. `cc:00.0`). The device ID is not needed for `gaudi_oam_cpld` and `gaudi_spi` on the Intel Gaudi3 system.
- If the execution "Status" field of the managed system shows SUCCESS, the console output of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
