# GetBmcInfo

Gets the BMC firmware image information from the managed system as well as the local BMC firmware image (with the `--file` option).

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetBmcInfo [--file <filename> [--extract_measurement]] [--showall]
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c GetBmcInfo [--file <filename> [--extract_measurement]] [--showall]
```

### Remote In-Band
```
saa -I Remote_RHI -u <username> -p <password> --oi <OS IP address> --ou <OS username> --op <OS password> [--remote_saa <remote SAA path>] -c GetBmcInfo [--file <filename> [--extract_measurement]] [--showall]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetBmcInfo [--file <filename> [--extract_measurement]] [--showall]
```

## Options

- `--file <file name>`: Reads the BMC information from the input BMC image file
- `--individually`: Gets information of BMC on each system with the corresponding configuration file individually
- `--file_only`: Works with `--file`, and only reads BMC information from the input image file
- `--extract_measurement`: Works with `--file`, and extracts the BMC image file measurement
- `--showall`: Displays all information

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBmcInfo --file Supermicro_BMC.bin
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetBmcInfo --file Supermicro_BMC.bin
[SAA_HOME]# ./saa -c GetBmcInfo --file Supermicro_ROT_BMC.bin --file_only
[SAA_HOME]# ./saa -c GetBmcInfo --file Supermicro_ROT_BMC.bin --file_only --extract_measurement
[SAA_HOME]# ./saa -c GetBmcInfo --file Supermicro_ROT_BMC.bin --showall
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.57 --ou root --op 111111 -c GetBmcInfo --file Supermicro_BMC.bin
```

### Remote In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Remote_RHI -u ADMIN -p PASSWORD --oi 192.168.34.57 --ou root --op 111111 -c GetBmcInfo --file Supermicro_BMC.bin
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetBmcInfo --file Supermicro_BMC.bin
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c GetBmcInfo --file Supermicro_BMC.bin
[SAA_HOME]# ./saa -I Remote_RHI -l SList.txt -c GetBmcInfo --file Supermicro_BMC.bin
```

## Output

### Non-RoT signed local BMC image
```
Managed system...........localhost
 BMC type.............X12_RoT_ATEN_AST2500
 BMC version..........00.23.37
 BMC ext. version.....01 00 00 (P)
 BMC build date.......2021/06/28
Local BMC image file...../home/user/BMC_X13AST2600-nonROT0501MS_20230807_01.01.13_STDsp.bin
 BMC UFFN.............BMC_X13AST2600-0501MS_20230807_01.01.13_STDsp.bin
 BMC type.............X13_ATEN_AST2600_1_1
 BMC version..........01.01.13
 BMC build date.......2023/08/07
 FW image.............Signed
 Signed Key.......NonRoT
```

### RoT signed local BMC image (Remote In-Band)
```
Local BMC image file......Supermicro_ROT_BMC.bin
 BMC UFFN..............BMC_X12AST2600-ROT-5201MS_20210317_01.00.00_STDsp.bin
 BMC type..............X12_RoT_ATEN_AST2600
 BMC version...........01.00.00
 FW image..............Signed
 Signed Key........RoT
```

### With --extract_measurement
```
Local BMC image file.....BMC_X12AST2600-ROT-6202MS_20220624_01.02.33_STDsd.bin
 BMC UFFN.............BMC_X12AST2600-ROT-6202MS_20220624_01.02.33_STDsd.bin
 BMC type.............X12_RoT_ATEN_AST2600_2
 BMC version..........01.02.33
 BMC build date.......2022/06/24
 FW image.............Signed
 Signed Key.......RoT
 Measurement......CE772709B937E6F256A09B9CEDFB9F7F4195B19143543964FD00C900BD73F1F36743724B34392B06D4D1D5542CFA0619C32AF960B93A3973A4F2101762A8698D
```

### With --showall
```
Local BMC image file..... BMC_X12AST2600-ROT-5201MS_20230204_09.20.72_BETsp.bin
 BMC UFFN.............BMC_X12AST2600-ROT-5201MS_20230204_09.20.72_BETsp.bin
 BMC type.............X12_RoT_ATEN_AST2600
 BMC version..........09.20.72
 BMC ext. version.....11 00 00 (beta_P)
 BMC build date.......2023/02/04
 BMC last reset time..2023-03-22T08:20:04Z
```

## Notes

- If the execution "Status" field for a managed system is SUCCESS, the BMC information of the managed system will be shown in its "Execution Message" section of the managed system in the created log file.
- The FW image signed key of a local BMC image displays: `Signed` (key signed by Super Micro Computer, Inc.), `Signed(U)` (signed by an unknown authority, not by Super Micro), `Signed(C)` (signed by the specified certificate, not by Super Micro), `Verification failed` (the signed information cannot be verified because the image is corrupted or incomplete), or the "FW image" field is not shown at all if there is no signed information in the image.
