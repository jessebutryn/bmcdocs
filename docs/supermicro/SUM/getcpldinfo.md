# GetCpldInfo

Use the "GetCpldInfo" command to get the CPLD firmware image information from the managed system as well as the local CPLD firmware image (with the --file option).

## Syntax

```
sum [[-i <IP or host name> | -I Redfish_HI] -u <username> -p <password>] -c
GetCpldInfo [--file <filename> [--file_only] [--extract_measurement]]
```

## Options

| Option | Augment | Description |
|--------|---------|-------------|
| --file | <filename> | Save the CPLD firmware image to the specified file. |
| --file_only | N/A | Only save the CPLD firmware image to file without displaying information. |
| --extract_measurement | N/A | Extract and display the measurement of the local CPLD image. |

## Examples

### OOB

```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetCpldInfo
```

### In-band

```
[SUM_HOME]# ./sum -c GetCpldInfo -I Redfish_HI -u ADMIN -p ADMIN --file CPLD.bin

[SUM_HOME]# ./sum -c GetCpldInfo -I Redfish_HI -u ADMIN -p ADMIN --file CPLD.bin
--extract_measurement
```

### Console Output

#### Basic Information

```
Managed system............192.168.34.56
 Motherboard CPLD version..........F1.00.BD
```

#### With Local File

```
Managed system...........192.168.34.56
 Motherboard CPLD version.........F1.00.BD
Local CPLD image file....CPLD.bin
 CPLD version.........F1.00.CD
 FW image.............Signed
 Signed Key.......RoT
```

#### With Measurement Extraction

```
Managed system...........192.168.34.56
 Motherboard CPLD version.........F0.09.46
Local CPLD image file....CPLD.bin
 CPLD version.........F0.0D.5A
 FW image.............Signed
 Signed Key.......RoT
 Measurement......7F3095B7E9ABC6F982719F7A293C68A02373C2BF5C6B7C160D5E980
D90E79708932E6F577B74814C244B81D76F2925F1F456E734CFE67AA8E9CA57C4DA894757
```

#### RoT Signing Status

| Type | Description |
|------|-------------|
| Signed | RoT is signed by Super Micro Computer, Inc. |
| Signed(U) | RoT is NOT signed by Super Micro Computer, Inc. but by an unknown authority. |
| Verification failed | The RoT signing in the image cannot be verified because the image is corrupted or incomplete. |

## Notes

- This command is only available on RoT systems of X12/H12 and later platforms.
- There could be multiple motherboard CPLD on a single motherboard, their information would be shown with indexed.