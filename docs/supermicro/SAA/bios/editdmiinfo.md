# EditDmiInfo

Updates (or adds) the specified DMI item in a DMI.txt file. When editing from an empty file, a new file is created. This is an alternative to manually editing a `DMI.txt` file obtained with `GetDmiInfo`. Specify an item using `--item_type`/`--item_name` or with `--shn` (short name); editable item types, names, and short names can be found in the DMI.txt file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c EditDmiInfo {--file <DMI.txt> --item_type <Item Type> --item_name <Item Name> | --shn <Item Short Name>} {--value <Item Value> | --default}
```

### In-Band
```
saa -c EditDmiInfo {--file <DMI.txt> --item_type <Item Type> --item_name <Item Name> | --shn <Item Short Name>} {--value <Item Value> | --default}
```

### Remote In-Band
```
saa -I Remote_INB --oi <OS IP address> --ou <OS username> --op <OS password> -c EditDmiInfo {--file <DMI.txt> --item_type <Item Type> --item_name <Item Name> | --shn <Item Short Name>} {--value <Item Value> | --default} [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c EditDmiInfo {--file <DMI.txt> --item_type <Item Type> --item_name <Item Name> | --shn <Item Short Name>} {--value <Item Value> | --default}
```

## Options

- `--file <file name>`: The DMI information file to be edited (or created if it does not exist)
- `--item_type <item type>`: Specifies the item type
- `--item_name <item name>`: Specifies the item name
- `--shn <short name>`: Specifies the item in short name format
- `--value <assignment value>`: Assigns the value to the item
- `--default`: Assigns the default value to the item

Either `[--item_type, --item_name]` or `[--shn]` is required. Either `[--value]` or `[--default]` is required.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c EditDmiInfo --file DMI.txt --item_type "System" --item_name "Version" --value "1.02"
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c EditDmiInfo --file DMI.txt --shn SYVS --value "1.02"
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c EditDmiInfo --file DMI.txt --shn SYVS --default
```

### In-Band
```bash
[SAA_HOME]# ./saa -c EditDmiInfo --file DMI.txt --shn SYVS --value 1.01
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c EditDmiInfo --file DMI.txt --shn SYVS --value 1.01 --remote_saa /root/saa
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c EditDmiInfo --file DMI.txt --item_type "System" --item_name "Version" --value "1.01"
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c EditDmiInfo --file DMI.txt --shn SYVS --value "1.01"
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c EditDmiInfo --file DMI.txt --shn SYVS --default
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c EditDmiInfo --file DMI.txt --shn SYVS --default
```

## Notes

- The supported editable DMI items may change for different BIOS versions. The version variable of the DMI.txt file must be the same as that of the managed system and should not be edited.
- If the execution "Status" field for a managed system (e.g., 192.168.34.56) is SUCCESS, its edited DMI information is updated in its output file, e.g., `DMI.txt.192.168.34.56`.
