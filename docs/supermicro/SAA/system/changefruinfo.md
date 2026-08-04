# ChangeFruInfo

Changes FRU (Field Replaceable Unit) information on the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c ChangeFruInfo {--item <item name> --value <assignment value> | --fru_version <FRU version>}
```

### In-Band
```
saa -c ChangeFruInfo {--item <item name> --value <assignment value> | --fru_version <FRU version>}
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c ChangeFruInfo {--item <item name> --value <assignment value> | --fru_version <FRU version>}
```

## Options

- `--item <item name>`: Updates the FRU information for the given FRU field:
    - `CT` = Chassis Type
    - `CP` = Chassis Part Number
    - `CS` = Chassis Serial Number
    - `BDT` = Board Mfg. Date/Time (`"YYYY/MM/DD HH:MM"`)
    - `BM` = Board Manufacturer
    - `BPN` = Board Product Name
    - `BS` = Board Serial Name
    - `BP` = Board Part Number
    - `PM` = Product Manufacturer
    - `PN` = Product Name
    - `PPM` = Product Part/Model Number
    - `PV` = Product Version
    - `PS` = Product Serial Number
    - `PAT` = Asset Tag
    - `ALL` = All Fields
- `--value <assignment value>`: Updates the value of the given FRU field. If the item is `ALL`, the format is `"<CT>,<CP>,<CS>,<BDT>,<BM>,<BPN>,<BS>,<BP>,<PM>,<PN>,<PPM>,<PV>,<PS>,<PAT>"`.
- `--fru_version <FRU version>`: Updates the FRU version.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeFruInfo --fru_version 00.01

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeFruInfo --item CT --value 0x01

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ChangeFruInfo --item ALL --value "0x01,2,3,2024/01/01 00:00,5,6,7,8,9,10,11,12,13,14"
```

### In-Band
```bash
[SAA_HOME]# ./saa -c ChangeFruInfo --fru_version 00.01

[SAA_HOME]# ./saa -c ChangeFruInfo --item CT --value 0x01
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ChangeFruInfo --item CT --value 0x01
```

`SList.txt`:
```
192.168.34.56 OS_Username OS_PASSWD
192.168.34.57 OS_Username OS_PrivateKey OS_Pvtkey_Password
```

## Output

### --item ALL
```
ChangeFruInfo command is completed.
Chassis Type (CT): 01
Chassis Part Number (CP): 2
Chassis Serial Number (CS): 3
Board mfg. Date/Time (BDT): 2024/01/01 00:00
Board Manufacturer Name (BM): 5
Board Product Name (BPN): 6
Board Serial Number (BS): 7
Board Part Number (BP): 8
Product Manufacturer (PM): 9
Product Name (PN): 10
Product Part/Model Number (PPM): 11
Product Version (PV): 12
Product Serial Number (PS): 13
Product Asset Tag (PAT): 14
```

### --item CT
```
ChangeFruInfo command is completed.
Chassis Type (CT): 01
Chassis Part Number (CP):
Chassis Serial Number (CS):
Board mfg. Date/Time (BDT): 2021/08/30 18:01
Board Manufacturer Name (BM): Supermicro
Board Product Name (BPN):
Board Serial Number (BS): WM218S011157
Board Part Number (BP):
Product Manufacturer (PM):
Product Name (PN):
Product Part/Model Number (PPM):
Product Version (PV):
Product Serial Number (PS):
Product Asset Tag (PAT):
```
