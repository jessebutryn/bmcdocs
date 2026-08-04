# FoundBmcDevices

Manages BMC devices previously found with `FindBmcDevices`. In-band only.

## Syntax

### In-Band
```
saa -c FoundBmcDevices --action { List | Clear | Copy --index <number separated by space> | CopyAll | SaveAs --file <file name> | Refresh }
```

## Actions

- **List**: Lists all found BMC devices.
- **Clear**: Clears all found BMC devices.
- **Copy**: Copies the found devices to the default managed group.
- **CopyAll**: Copies all found devices to the default managed group.
- **SaveAs**: Saves the results of found BMC devices to a file.
- **Refresh**: Refreshes the result of found BMC devices.

## Options

- `--action <action>`: Sets action to List, Clear, Copy, CopyAll, SaveAs, or Refresh.
- `--file <file name>` (Optional): Specifies the name of the file to write. Required when using the SaveAs action.
- `--index <index>` (Optional): Specifies the indices of the host to be copied. Required when using the Copy action.

## Examples

### In-Band
```bash
[SAA_HOME]# ./saa -c FoundBmcDevices --action List

[SAA_HOME]# ./saa -c FoundBmcDevices --action Clear
```

## Output

### Action List
```
10.184.17.12 cannot login by ADMIN/ADMIN
10.184.17.13 cannot login by ADMIN/ADMIN
Managed hosts loaded.Found hosts loaded.
Found IPMI Devices
------------------
```
