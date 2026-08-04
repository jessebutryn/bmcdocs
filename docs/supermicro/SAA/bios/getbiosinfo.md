# GetBiosInfo

Gets the BIOS firmware image information from the managed system as well as the local BIOS firmware image (with the `--file` option).

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetBiosInfo [--showall] [--extract_measurement]
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c GetBiosInfo [--file <filename> [--file_only]] [--showall] [--extract_measurement]
```

### Remote In-Band
```
saa {-I Remote_INB | -I Remote_RHI -u <username> -p <password>} --oi <OS IP address> --ou <OS username> --op <OS password> -c GetBiosInfo [--file <filename> [--file_only]] [--showall] [--extract_measurement] [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetBiosInfo [--file <filename>] [--showall]
```

## Options

- `--file <file name>`: Reads BIOS information from an input BIOS image file
- `--individually`: Gets each BIOS with its corresponding image file individually
- `--showall`: Prints the BIOS version, BIOS revision and BIOS OEM FID information (also prints the last BMC reset time)
- `--file_only`: Works with `--file`, and only reads BIOS information from the input image file
- `--extract_measurement`: Works with `--file`, extract BIOS image file measurement
- `--redfish`: Enables support for pure Redfish

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBiosInfo --file Supermicro_BIOS_signed.bin
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetBiosInfo --file Supermicro_BIOS_signed.bin --file_only
[SAA_HOME]# ./saa -c GetBiosInfo --file Supermicro_BIOS.bin --showall
[SAA_HOME]# ./saa -c GetBiosInfo --file Supermicro_BIOS.bin --file_only --extract_measurement
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.57 --ou root --op 111111 -c GetBiosInfo --remote_saa /root/saa
```

### Remote In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Remote_RHI -u ADMIN -p PASSWORD --oi 192.168.34.57 --ou root --op 111111 -c GetBiosInfo --remote_saa /root/saa
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetBiosInfo --file Supermicro_BIOS.bin
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c GetBiosInfo --file Supermicro_BIOS.bin
```

## Output

### In-Band with local BIOS image (secure flash signed)
```
Managed system...........192.168.34.56
 Board ID.............0660
 BIOS build date......2012/10/17
Local BIOS image file.... Supermicro_BIOS_signed.bin
 Board ID.............0988
 BIOS build date......2018/5/7
 FW image.............Signed
 Signed Key.......SecureFlash
```

### With --showall
```
Local BIOS image file....Supermicro_BIOS_signed.bin
 Board ID.............1B6A
 BIOS build date......2021/01/12
 FW image.............Signed
 Signed Key.......RoT
Managed system:
 Board ID.............0660
 BIOS build date......2012/10/17
 BIOS version.........1.0
 BIOS revision........1.8
Local BIOS image file....Supermicro_BIOS.bin
 Board ID.............1B4A
 BIOS build date......2021/03/11
 FW image.............Signed
 Signed Key.......RoT
 BIOS version.........1.0a
 BIOS revision........5.22
 FW global version: 0
 RC version: 20.P80
 SPS version: 4.4.4.53
 CPU signature: 00 06 06 a4
 Description: IceLakeServer L0
 Version: 0B000280
 CPU signature: 00 06 06 a5
 Description: IceLakeServer C0
 Version: 0C0002B0
 CPU signature: 00 06 06 a6
 Description: IceLakeServer D0
 Version: 0D000260
 ............
 BIOS build date: 2021/03/11
 BIOS version: 1.0a
 UUID: 936B704B-2D82-EB11-9FAD-0CC47AFBDDC6
 PMEM version: 02.02.00.1553
 BIOS unique name: BIOS_X12SPI-1B4A_20210311_1.0a_STDsp.bin
```

### Multiple Systems OOB (with Remote In-Band system in list)
```
Local BIOS image file...................Supermicro_BIOS.bin
 Board ID............................1B6A
 BIOS build date.....................2022/05/27
 FW image............................Signed
 Signed Key......................RoT
 Measurement.....................FB0DC09383104F49834E2E903F46F365259CB5986D97F0F3D9DB5945E0D0DFD59F8511F6857E915B414A1B9A30071EF5D99018144033DCC80464B951E555402B
Start Remote In-Band execution on 192.168.34.57:
================================================================================
SuperServer Automation Assistant 1.0.0 (2023/08/18) (x86_64)
Copyright(C) 2023 Super Micro Computer, Inc. All rights reserved.
Reading BIOS flash ..................... (100%)
Managed system:
 Board ID............................1A07
 BIOS build date.....................2021/05/25
================================================================================
Getting file 'remote_inband/2022-11-03_17-38-55_192.168.34.57/saa.log' from '/root/saa_remote_inband/2022-11-03_17-37-49/saa.log' on 192.168.34.57.
```

## Notes

- The SecureFlash-signed key of the local BIOS image can show `Signed` (signed by Super Micro Computer, Inc.), `Signed(U)` (signed by an unknown authority), or the "FW image" field may not be shown at all if no secure flash signing is present in the image.
- A RoT-signed key of the local BIOS image can similarly show `Signed`, `Signed(U)`, or not be shown if the RoT signing cannot be verified because the image is corrupted or incomplete.
- If the execution "Status" field of a managed system is SUCCESS, the BIOS information of the managed system will be shown in its "Execution Message" section in the created log file.
- With the Seamless Update capsule feature (X13 RoT platforms or later), `--file CAPSULE_FILE.bin --file_only` shows capsule information of the local file; `--file BIOS_FILE.bin --showall --file_only` shows all capsule information supported by the current local BIOS file; running against the managed system (OOB or in-band Redfish_HI) with `--file CAPSULE_FILE.bin` shows the corresponding capsule information on the managed system, and with `--showall` shows all capsule information types supported by the managed system.
