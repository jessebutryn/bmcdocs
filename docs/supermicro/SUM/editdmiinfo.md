# EditDmiInfo

Edits DMI (Desktop Management Interface) items in a DMI configuration file. Updates or adds specified DMI items in the file.

## Syntax

### OOB and In-Band
```
sum [-i <IP or host name> -u <username> -p <password>] -c EditDmiInfo --file <DMI.txt> [--item_type <Item Type> --item_name <Item Name> | --shn <Item Short Name>] [--value <Item Value> | --default]
```

### Remote In-Band
```
sum -I Remote_INB --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c EditDmiInfo --file <DMI.txt> [--item_type <Item Type> --item_name <Item Name> | --shn <Item Short Name>] [--value <Item Value> | --default] [--remote_sum <remote sum path>]
```

## Options

- `--file <DMI.txt>`: Required. DMI configuration file to edit
- `--item_type <Item Type>`: DMI item type (e.g., "System")
- `--item_name <Item Name>`: DMI item name (e.g., "Version")
- `--shn <Item Short Name>`: DMI item short name (alternative to item_type + item_name)
- `--value <Item Value>`: New value for the DMI item
- `--default`: Reset the DMI item to its default value
- `--remote_sum <remote sum path>`: Path to remote SUM executable

## Examples

### OOB
```bash
# Edit using item type and name
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c EditDmiInfo --file DMI.txt --item_type "System" --item_name "Version" --value "1.02"

# Edit using short name
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c EditDmiInfo --file DMI.txt --shn SYVS --value "1.02"

# Reset to default
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c EditDmiInfo --file DMI.txt --shn SYVS --default
```

### In-Band
```bash
[SUM_HOME]# ./sum -c EditDmiInfo --file DMI.txt --shn SYVS --value 1.01
```

### Remote In-Band
```bash
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c EditDmiInfo --file DMI.txt --shn SYVS --value 1.01 --remote_sum /root/sum
```

## Notes

- Only updates the specified DMI item in the file
- Creates a new file if editing from an empty file
- Editable item types, names, and short names are found in the DMI.txt file
- Get DMI.txt file first using GetDmiInfo command
- Changes take effect after system reboot or power up when applied with ChangeDmiInfo