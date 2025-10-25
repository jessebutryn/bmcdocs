# Attestation

Manages remote attestation measurement files on managed systems. Remote attestation provides digital signatures for measurement files containing system states like firmware version, measurements, configuration data, and hardware information.

## Syntax

### OOB and In-Band
```
sum [<-i <IP or host name> | -I Redfish_HI> -u <username> -p <password>] -c Attestation --action <action> [--file <filename>] [--ref <filename>] [--overwrite] [--item <item name>] [--showall] [--file_only] [--nonce <nonce>]
```

### Remote In-Band
```
sum -I Remote_RHI -u <username> -p <password> --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c Attestation --action <action> [--file <filename>] [--ref <filename>] [--overwrite] [--item <item name>] [--showall] [--file_only] [--nonce <nonce>] [--remote_sum <remote sum path>]
```

## Actions

- **Dump**: Create and download a measurement file from the managed system
- **List**: List existing measurement files on the managed system
- **Download**: Download an existing measurement file from the managed system
- **Delete**: Delete an existing measurement file on the managed system
- **GetInfo**: Get information from local measurement files (in-band only)
- **Compare**: Compare managed system or local measurement file with a referenced measurement file

## Options

- `--action <action>`: Required. Action to perform (Dump, List, Download, Delete, GetInfo, Compare)
- `--file <filename>`: Measurement file name (used differently per action)
- `--ref <filename>`: Referenced measurement file for comparison
- `--overwrite`: Overwrite existing files
- `--item <item name>`: Specific item to display (GetInfo action only)
- `--showall`: Display all items in measurement file (GetInfo action only)
- `--file_only`: Work with local files only (GetInfo action only)
- `--nonce <nonce>`: Nonce value for measurement generation (Dump and Compare actions)
- `--remote_sum <remote sum path>`: Path to remote SUM executable

## Examples

### OOB
```bash
# Dump measurement with custom nonce
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c Attestation --action Dump --file measurement.bin --overwrite --nonce MY_NONCE_XXXX

# Dump measurement with default filename
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c Attestation --action Dump

# List measurement files
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c Attestation --action List
```

### In-Band
```bash
# Download measurement file
[SUM_HOME]# ./sum -I Redfish_HI -u ADMIN -p PASSWORD -c Attestation --action Download --file measurement.bin

# Delete measurement file
[SUM_HOME]# ./sum -I Redfish_HI -u ADMIN -p PASSWORD -c Attestation --action Delete --file measurement.bin

# Get info from local measurement file
[SUM_HOME]# ./sum -c Attestation --action GetInfo --file_only --file measurement.bin
```

### Remote In-Band
```bash
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c Attestation --action Download --file measurement.bin
```

### Remote In-Band through Host Interface
```bash
[SUM_HOME]# ./sum -I Remote_RHI -u ADMIN -p PASSWORD --oi 192.168.34.56 --ou root --op 111111 -c Attestation --action Download --file measurement.bin
```

## Output Examples

### Measurement File Info
```
Measurement..............measurement.bin
 Nonce................2022-04-12T11:20:25+08:00
 Signature............Signed
 Certificate Chain....Verified
```

### With Extract Certificate
```
Measurement..............measurement.bin
 Nonce................2022-04-12T11:20:25+08:00
 Signature............Signed
 Certificate Chain....Verified
Device Identity Certificate PEM chain file "chain.pem" is created.
```

### Specific Item
```
Measurement..............measurement.bin
 Nonce................2022-04-12T11:20:25+08:00
 Signature............Signed
 Certificate Chain....Verified
 Item: BMC_ACT_MEAS
 Description: BMC Firmware Measurement
 Value: A30CFFC59284658300654B8CDD5144B7C8CCDF3540B52EAF98FE0B7A3A8A4BB1E7FEA...
```

### Show All Items
```
 Item: <Item Name>
 Description: <Item Description>
 Value: <Item Value>
```

## Notes

- This command is only available for OOB and in-band usage restricted to the Redfish host interface when managing measurement files on the managed system
- For Dump action: Without `--file`, measurement file is saved with the same name as on the managed system
- For Dump and Compare actions: Without `--nonce`, current OS time is used as default nonce
- GetInfo action is in-band only and requires `--file` and `--file_only`
- `--item` and `--showall` are mutually exclusive for GetInfo action
- `--root_cert` and `--extract_cert` are only for GetInfo action

## Signature Status

### Measurement File Signature
- **Signed**: Signature is signed by Device Attestation Key and verified by Device Attestation Public Key
- **Verification failed**: Signature cannot be verified

### Certificate Chain
- **Verified**: Device Identity Certificate Chain verified back to Root CA
- **Verification failed**: Certificate chain cannot be verified

### Root Certificates
- **Matched**: Root CA Certificate matches input certificate file
- **Mismatched**: Root CA Certificate does not match input certificate file
