# GetBiosInfo

Gets the BIOS firmware image information from the managed system and/or local BIOS firmware image file.

## Syntax

### OOB and In-Band
```
sum [[-i <IP or host name> | -I Redfish_HI] -u <username> -p <password>] -c GetBiosInfo [--file <filename> [--file_only]] [--showall] [--extract_measurement]
```

### Remote In-Band
```
sum [-I Remote_INB | -I Remote_RHI -u <username> -p <password>] --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c GetBiosInfo [--file <filename> [--file_only]] [--showall] [--extract_measurement] [--remote_sum <remote sum path>]
```

## Options

- `--file <filename>`: Reads BIOS information from an input BIOS image file
- `--file_only`: Works with `--file`, reads BIOS information from the input image file only
- `--showall`: Displays all available information
- `--extract_measurement`: Works with `--file`, extracts BIOS image file measurement
- `--remote_sum <remote sum path>`: Path to remote SUM executable (for remote in-band)

## Examples

### OOB
```bash
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBiosInfo --file Supermicro_BIOS_signed.rom
```

### In-Band
```bash
[SUM_HOME]# ./sum -c GetBiosInfo --file Supermicro_BIOS_signed.rom --file_only
[SUM_HOME]# ./sum -c GetBiosInfo --file Supermicro_BIOS.rom --showall
[SUM_HOME]# ./sum -c GetBiosInfo --file Supermicro_BIOS.rom --file_only --extract_measurement
```

### Remote In-Band
```bash
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.57 --ou root --op 111111 -c GetBiosInfo --remote_sum /root/sum
```

### Remote In-Band through Redfish Host Interface
```bash
[SUM_HOME]# ./sum -I Remote_RHI -u ADMIN -p PASSWORD --oi 192.168.34.57 --ou root --op 111111 -c GetBiosInfo --remote_sum /root/sum
```

## Output Examples

### SecureFlash Signed BIOS
```
Managed system...........192.168.34.56
 Board ID.............0660
 BIOS build date......2012/10/17
Local BIOS image file.... Supermicro_BIOS_signed.rom
 Board ID.............0988
 BIOS build date......2018/5/7
 FW image.............Signed
 Signed Key.......SecureFlash
```

### RoT Signed BIOS
```
Local BIOS image file....Supermicro_BIOS_signed.rom
 Board ID.............1B6A
 BIOS build date......2021/01/12
 FW image.............Signed
 Signed Key.......RoT
```

### With Showall
```
Managed system:
 Board ID.............0660
 BIOS build date......2012/10/17
 BIOS version.........1.0
 BIOS revision........1.8
Local BIOS image file....Supermicro_BIOS.rom
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
 ...
 BIOS unique name: BIOS_X12SPI-1B4A_20210311_1.0a_STDsp.bin
```

### With Measurement
```
Local BIOS image file...................Supermicro_BIOS.rom
 Board ID............................1B6A
 BIOS build date.....................2022/05/27
 FW image............................Signed
 Signed Key......................RoT
 Measurement.....................FB0DC09383104F49834E2E903F46F365259CB598...
```

## Signing Status Descriptions

### SecureFlash Key Types
- **Signed**: Secure flash is signed by Super Micro Computer, Inc.
- **Signed(U)**: Secure flash is NOT signed by Super Micro Computer, Inc., but by an unknown authority
- **(Not shown)**: No secure flash signing in the image

### RoT Key Types
- **Signed**: RoT is signed by Super Micro Computer, Inc.
- **Signed(C)**: RoT is verified by the specified certificate
- **Signed(U)**: RoT is NOT signed by Super Micro Computer, Inc. but by an unknown authority
- **Verification failed**: RoT signing cannot be verified
