# ChangeFruInfo

Changes FRU (Field Replaceable Unit) information on the managed system.

## Syntax

```
sum [-i <IP or host name>] -u <username> -p <password> -c ChangeFruInfo --item <item name> --value <assignment value>
```

## Options

- `--item <item name>`: Required. FRU item to change (e.g., CT for Chassis Type)
- `--value <assignment value>`: Required. New value for the FRU item

## Examples

### OOB
```bash
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeFruInfo --item CT --value 0x01
```

### In-Band
```bash
[SUM_HOME]# ./sum -c ChangeFruInfo --item CT --value 0x01
```

## Output

The command displays "ChangeFruInfo command is completed." followed by the updated FRU information including:

- Chassis Type
- Chassis Part Number
- Chassis Serial Number
- Mfg. Date
- Board Manufacturer
- Board Product Name
- Board Serial Number
- Board Part Number
- Manufacturer Name
- Product Name
- Product Part Number
- Product Version
- Product Serial Number
- Asset Tag

## Notes

- Only available for OOB usage
- Changes take effect immediately
