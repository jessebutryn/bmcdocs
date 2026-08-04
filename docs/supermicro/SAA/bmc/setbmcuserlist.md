# SetBmcUserList

Sets the current BMC user list for the target system. The action performed depends on the `--action` value.

## Actions

- `Add` (`1`): Adds a new BMC user
- `Del` (`2`): Deletes a BMC user
- `Level` (`3`): Changes a BMC user's privilege
- `SetPwd` (`4`): Changes a BMC user password
- `Test` (`5`): Verifies a BMC user login
- `EnableType` (`6`): Activates a BMC user account type
- `EnableAccount` (`7`): Activates a BMC user status
- `EditUserName` (`8`): Edits a BMC user name

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SetBmcUserList --action add --user_id <userid> --user_name <username> --user_password <userpassword> --user_privilege <userprivilege> [--user_status <status>] [--manage_account_type <type:status> [--ap <protocol> --pp <protocol> --ak <key> --pk <key>]]
saa -i <IP or host name> -u <username> -p <password> -c SetBmcUserList --action <action> --user_id <userid> [--user_name <username>] [--user_password <userpassword>] [--user_privilege <userprivilege>]
saa -i <IP or host name> -u <username> -p <password> -c SetBmcUserList --action Test --user_name <username> --user_password <userpassword>
saa -i <IP or host name> -u <username> -p <password> -c SetBmcUserList --action EnableType --user_id <userid> {--account_type <type> --account_type_status <status> | --manage_account_type <type:status>} [--ap <protocol> --pp <protocol> --ak <key> --pk <key>]
saa -i <IP or host name> -u <username> -p <password> -c SetBmcUserList --action EnableAccount --user_id <userid> --user_status <status>
saa -i <IP or host name> -u <username> -p <password> -c SetBmcUserList --action EditUserName --user_id <userid> --user_name <username>
```

### In-Band
```
saa -c SetBmcUserList --action add --user_id <userid> --user_name <username> --user_password <userpassword> --user_privilege <userprivilege>
saa -I Redfish_HI -u <username> -p <password> -c SetBmcUserList --action add --user_id <userid> --user_name <username> --user_password <userpassword> --user_privilege <userprivilege> [--user_status <status>] [--manage_account_type <type:status> [--ap <protocol> --pp <protocol> --ak <key> --pk <key>]]
saa -c SetBmcUserList --action <action> --user_id <userid> [--user_name <username>] [--user_password <userpassword>] [--user_privilege <userprivilege>]
saa -I Redfish_HI -u <username> -p <password> -c SetBmcUserList --action Test --user_name <username> --user_password <userpassword>
saa -I Redfish_HI -u <username> -p <password> -c SetBmcUserList --action EnableType --user_id <userid> {--account_type <type> --account_type_status <status> | --manage_account_type <type:status>} [--ap <protocol> --pp <protocol> --ak <key> --pk <key>]
saa -I Redfish_HI -u <username> -p <password> -c SetBmcUserList --action EnableAccount --user_id <userid> --user_status <status>
saa -I Redfish_HI -u <username> -p <password> -c SetBmcUserList --action EditUserName --user_id <userid> --user_name <username>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SetBmcUserList --action add --user_id <userid> --user_name <username> --user_password <userpassword> --user_privilege <userprivilege> [--user_status <status>] [--manage_account_type <type:status> [--ap <protocol> --pp <protocol> --ak <key> --pk <key>]]
saa -l <system list file> [-u <username> -p <password>] -c SetBmcUserList --action <action> --user_id <userid> [--user_name <username>] [--user_password <userpassword>] [--user_privilege <userprivilege>]
saa -l <system list file> [-u <username> -p <password>] -c SetBmcUserList --action Test --user_name <username> --user_password <userpassword>
saa -l <system list file> [-u <username> -p <password>] -c SetBmcUserList --action EnableType --user_id <userid> {--account_type <type> --account_type_status <status> | --manage_account_type <type:status>} [--ap <protocol> --pp <protocol> --ak <key> --pk <key>]
saa -l <system list file> [-u <username> -p <password>] -c SetBmcUserList --action EnableAccount --user_id <userid> --user_status <status>
saa -l <system list file> [-u <username> -p <password>] -c SetBmcUserList --action EditUserName --user_id <userid> --user_name <username>
```

## Options

- `--action <action>`: Required. Sets action to `1`/Add, `2`/Del, `3`/Level, `4`/SetPwd, `5`/Test, `6`/EnableType, `7`/EnableAccount, `8`/EditUserName
- `--user_id <user ID>`: The BMC user ID
- `--user_name <user name>`: The BMC user name
- `--user_password <user password>`: The BMC user password
- `--user_privilege <user privilege>`: Privilege level — Administrator: `4`, Operator: `3`, User: `2`, Callback: `1`, No Access: `15` (Callback is not supported on an open BMC system; No Access is not supported)
- `--user_status <user enable>`: Manages the status of a BMC user: `0` = Disable, `1` = Enable
- `--account_type <account type>`: Supported account type for BMC management: `0` = SNMP
- `--account_type_status <account type status>`: Manages account type status: `0` = Disable, `1` = Enable
- `--ap <authentication protocol>`: `0` = MD5, `1` = SHA
- `--pp <private protocol>`: `0` = DES, `1` = AES
- `--ak <authentication key>`: The authentication key
- `--pk <private key>`: The private key
- `--manage_account_type <manage account type>`: Manages the status of account types; format `"SNMP:Enable,Redfish:Disable"`. Supported account types: Redfish, SNMP

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBmcUserList --action Add --user_id 3 --user_name NAME3 --user_password PASSWORD3 --user_privilege 3 --user_status Disable --manage_account_type SNMP:Enable,Redfish:Disable --ap SHA --pp DES --ak AKEY3 --pk PKEY3
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBmcUserList --action Del --user_id 3
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBmcUserList --action Level --user_id 3 --user_privilege 3
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBmcUserList --action SetPwd --user_id 3 --user_password PASSWORD3
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBmcUserList --action Test --user_name NAME3 --user_password PASSWORD3
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBmcUserList --action EnableType --user_id 3 --account_type SNMP --account_type_status enable --ap 0 --pp DES --ak KEY --pk KEY
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBmcUserList --action EnableAccount --user_id 3 --user_status Disable
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBmcUserList --action EditUserName --user_id 3 --user_name NAME4
```

### In-Band
```bash
[SAA_HOME]# ./saa -c SetBmcUserList --action 1 --user_id 3 --user_name NAME3 --user_password PASSWORD3 --user_privilege 3
[SAA_HOME]# ./saa -c SetBmcUserList --action 2 --user_id 3
[SAA_HOME]# ./saa -c SetBmcUserList --action 3 --user_id 3 --user_privilege 3
[SAA_HOME]# ./saa -c SetBmcUserList --action 4 --user_id 3 --user_password PASSWORD3
```

### In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c SetBmcUserList --action 1 --user_id 3 --user_name NAME3 --user_password PASSWORD3 --user_privilege 3 --user_status Disable --manage_account_type SNMP:Enable,Redfish:Disable --ap SHA --pp 1 --ak KEY --pk KEY
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c SetBmcUserList --action 5 --user_name NAME3 --user_password PASSWORD3
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c SetBmcUserList --action 6 --user_id 3 --account_type SNMP --account_type_status enable --ap SHA --pp 1 --ak KEY --pk KEY
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c SetBmcUserList --action 6 --user_id 3 --manage_account_type SNMP:Enable,Redfish:Disable --ap SHA --pp 1 --ak KEY --pk KEY
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c SetBmcUserList --action 7 --user_id 3 --user_status Disable
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c SetBmcUserList --action 8 --user_id 3 --user_name NAME4
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetBmcUserList --action Add --user_id 3 --user_name NAME3 --user_password PASSWORD3 --user_privilege 3 --user_status Disable --manage_account_type SNMP:Enable,Redfish:Disable --ap SHA --pp DES --ak AKEY3 --pk PKEY3
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetBmcUserList --action Del --user_id 3
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l SList.txt -c SetBmcUserList --action 1 --user_id 3 --user_name NAME3 --user_password PASSWORD3 --user_privilege 3
```

### Multiple Systems Remote In-Band through Redfish Host Interface
```bash
[SAA_HOME]# ./saa -I Remote_RHI -l SList.txt -c SetBmcUserList --action 1 --user_id 3 --user_name NAME3 --user_password PASSWORD3 --user_privilege 3 --user_status Disable --manage_account_type SNMP:Enable,Redfish:Disable --ap SHA --pp 1 --ak KEY --pk KEY
```

## Notes

- The "No Access" user privilege is not supported.
- `--action EnableType` and `--action EnableAccount` are not supported on platforms before X12/H12.
- If the execution "Status" field for a managed system is SUCCESS, the console output of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
