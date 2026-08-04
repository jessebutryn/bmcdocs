# GetCpldInfo

Gets the motherboard CPLD firmware image information from the managed system, as well as information from a local CPLD firmware image (with the `--file` option).

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetCpldInfo [--file <filename> [--extract_measurement]]
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c GetCpldInfo [--file <filename> [--file_only] [--extract_measurement]]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetCpldInfo [--file <filename> [--extract_measurement]]
```

## Options

- `--individually`: (Optional) Gets each CPLD with its corresponding image file individually.
- `--file <file name>`: (Optional) Reads the CPLD information from an input CPLD image file.
- `--file_only`: (Optional) Works with the `--file` option, and only reads CPLD information from the input image file.
- `--extract_measurement`: (Optional) Works with the `--file` option, extract CPLD image file measurement if supported.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetCpldInfo
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetCpldInfo -I Redfish_HI -u ADMIN -p ADMIN --file CPLD.bin

[SAA_HOME]# ./saa -c GetCpldInfo -I Redfish_HI -u ADMIN -p ADMIN --file CPLD.bin --extract_measurement
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetCpldInfo --file CPLD.bin
```

## Output

### Basic Information
```
Managed system.......................192.168.34.56
 Motherboard CPLD version.........F1.00.BD
```

### With Local File
```
Managed system.......................192.168.34.56
 Motherboard CPLD version.........F1.00.BD
Local CPLD image file................CPLD.bin
 CPLD version.....................F1.00.CD
 FW image.........................Signed
 Signed Key...................RoT
```

### With Measurement Extraction
```
Managed system.......................192.168.34.56
 Motherboard CPLD version.........F0.09.46
Local CPLD image file................CPLD.bin
 CPLD version.....................F0.0D.5A
 FW image.........................Signed
 Signed Key...................RoT

Measurement..................7F3095B7E9ABC6F982719F7A293C68A02373C2BF5C6B7C160D5E
980D90E79708932E6F577B74814C244B81D76F2925F1F456E734CFE67AA8E9CA57C4DA894757
```

### RoT Signing Status

| Type | Description |
|------|-------------|
| Signed | The key is signed by Super Micro Computer, Inc. |
| Signed(U) | The key is NOT signed by Super Micro Computer, Inc., but by an unknown authority. |
| Verification failed | The signed information in the image cannot be verified, because the image is corrupted or incomplete. |

## Notes

- If the execution "Status" field of the managed system shows SUCCESS, the console output of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
- There could be multiple motherboard CPLDs on a single motherboard; their information is shown indexed.
