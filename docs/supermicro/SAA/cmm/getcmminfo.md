# GetCmmInfo

Gets the CMM firmware image information from the managed system, as well as information from a local CMM firmware image file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetCmmInfo [--file <filename>] [--showall]
```

### In-Band
```
saa -c GetCmmInfo --file <filename> --file_only
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetCmmInfo [--file <filename>] [--showall]
```

## Options

- `--file <file name>`: Reads the CMM information from an input CMM image file (optional).
- `--individually`: Gets each CMM with its corresponding image file individually (optional).
- `--showall`: Prints the BIOS, BMC, and ARM SAA information of the managed Blade system (optional).
- `--file_only`: Works with `--file`, and only reads CMM information from the input image file (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetCmmInfo --file Supermicro_CMM.bin
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetCmmInfo --file Supermicro_CMM.bin
```

## Output

```
Managed system...........192.168.34.56
 CMM type.............MicroCMM
 CMM version..........09.01
 ARM SAA version......1.0.0 (2021/12/10) (ARM)
 Dummy switch version.01.02
Local CMM image file.....Supermicro_CMM.bin
 CMM type.............MicroCMM
 CMM version..........09.10
```

### With --showall

```
Blade ID: B6
==============
Node ID: 1
 Board model..........BH12SSi
 Status...............Normal
 BMC IP...............192.168.34.57
 BIOS version.........2.3a
 BIOS build date......2021/09/14
 BMC version..........75.00.06
 ARM SAA version......1.0.0 (2021/12/10) (ARM)
```

## Notes

- Three models of 7U SuperBlade CMMs — SBM-CMM-001, BMB-CMM-002 (mini-CMM), and SBM-CMM-003 — are no longer supported.
- If the Status field for a managed system shows SUCCESS, the CMM information of the managed system is shown in the Execution Message section of the created log file.
