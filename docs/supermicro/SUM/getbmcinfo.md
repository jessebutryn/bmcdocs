# GetBmcInfo

Gets the BMC firmware image information from the managed system as well as the BMC firmware image.

## Syntax

### OOB and In-Band
```
sum [[-i <IP or host name> | -I Redfish_HI] -u <username> -p <password>] -c GetBmcInfo [--file <filename> [--file_only] [--extract_measurement] [--showall]]
```

### Remote In-Band
```
sum [-I Remote_INB | -I Remote_RHI -u <username> -p <password>] --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c GetBmcInfo [--file <filename> [--file_only] [--extract_measurement] [--remote_sum <remote sum path>]]
```

## Options

- `--file <filename>`: Reads the BMC information from an input BMC image file
- `--file_only`: Works with `--file`, and only reads BMC information from the input image file
- `--extract_measurement`: Works with `--file`, extracts BMC image file measurement
- `--showall`: Displays all information
- `--remote_sum <remote sum path>`: Path to remote SUM executable (for remote in-band)

## Examples

### OOB
```bash
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBmcInfo --file Supermicro_BMC.rom
```

### In-Band
```bash
[SUM_HOME]# ./sum -c GetBmcInfo --file Supermicro_BMC.rom
```

### File Only
```bash
[SUM_HOME]# ./sum -c GetBmcInfo --file Supermicro_BMC.rom --file_only
```

### Extract Measurement
```bash
[SUM_HOME]# ./sum -c GetBmcInfo --file Supermicro_ROT_BMC.rom --file_only --extract_measurement
```

### Show All
```bash
[SUM_HOME]# ./sum -c GetBmcInfo --file Supermicro_BMC.rom --showall
```

### Remote In-Band
```bash
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.57 --ou root --op 111111 -c GetBmcInfo --file Supermicro_BMC.rom
```

## Output

The output varies depending on the options and BMC type. Examples include:

### Non-RoT Signed BMC
```
Managed system............localhost
 BMC type..............X11_ATEN_AST2500_2
 BMC version...........12.63.00
 BMC ext. version......01 00 00
Local BMC image file......Supermicro_BMC.rom
 BMC type..............X11_ATEN_AST2500_2
 BMC version...........12.63.00
 FW image..............Signed
 Signed Key........NonRoT
```

### RoT Signed BMC
```
Local BMC image file...... Supermicro_ROT_BMC.rom
 BMC UFFN..............BMC_X12AST2600-ROT-5201MS_20210317_01.00.00_STDsp.bin
 BMC type..............X12_RoT_ATEN_AST2600
 BMC version...........01.00.00
 FW image..............Signed
 Signed Key........RoT
```

### With Measurement
```
Local BMC image file.....BMC_X12AST2600-ROT-6202MS_20220624_01.02.33_STDsd.bin
 BMC UFFN.............BMC_X12AST2600-ROT-6202MS_20220624_01.02.33_STDsd.bin
 BMC type.............X12_RoT_ATEN_AST2600_2
 BMC version..........01.02.33
 BMC build date.......2022/06/24
 FW image.............Signed
 Signed Key.......RoT
 Measurement......CE772709B937E6F256A09B9CEDFB9F7F4195B19143543964FD00C90
0BD73F1F36743724B34392B06D4D1D5542CFA0619C32AF960B93A3973A4F2101762A8698D
```

### With Showall
```
Local BMC image file..... BMC_X12AST2600-ROT-5201MS_20230204_09.20.72_BETsp.bin
 BMC UFFN.............BMC_X12AST2600-ROT-5201MS_20230204_09.20.72_BETsp.bin
 BMC type.............X12_RoT_ATEN_AST2600
 BMC version..........09.20.72
 BMC ext. version.....11 00 00 (beta_P)
 BMC build date.......2023/02/04
 BMC last reset time..2023-03-22T08:20:04Z
```
