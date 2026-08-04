# SetCmmUserList

Sets the current CMM user list for the target system: add or delete a CMM user, change a user's privilege or password, test a user login, or enable a CMM user account type.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SetCmmUserList --action add --user_id <userid> --user_name <username> --user_password <userpassword> --user_privilege <userprivilege>
saa -i <IP or host name> -u <username> -p <password> -c SetCmmUserList --action <action> --user_id <userid> [--user_name <username>] [--user_password <userpassword>] [--user_privilege <userprivilege>]
saa -i <IP or host name> -u <username> -p <password> -c SetCmmUserList --action Test --user_name <username> --user_password <userpassword>
saa -i <IP or host name> -u <username> -p <password> -c SetCmmUserList --action EnableType --user_id --account_type <type> --account_type_status <status> [--ap <protocol> --pp <protocol> --ak <key> --pk <key>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SetCmmUserList --action add --user_id <userid> --user_name <username> --user_password <userpassword> --user_privilege <userprivilege>
saa -l <system list file> [-u <username> -p <password>] -c SetCmmUserList --action <action> --user_id <userid> [--user_name <username>] [--user_password <userpassword>] [--user_privilege <userprivilege>]
saa -l <system list file> [-u <username> -p <password>] -c SetCmmUserList --action Test --user_name <username> --user_password <userpassword>
saa -l <system list file> [-u <username> -p <password>] -c SetCmmUserList --action EnableType --user_id --account_type <type> --account_type_status <status> [--ap <protocol> --pp <protocol> --ak <key> --pk <key>]
```

## Actions

- **Add** (`1`): Adds a new CMM user.
- **Del** (`2`): Deletes a CMM user.
- **Level** (`3`): Changes a CMM user's privilege.
- **SetPwd** (`4`): Changes a CMM user's password.
- **Test** (`5`): Verifies a CMM user login.
- **EnableType** (`6`): Activates a CMM user account type.

## Options

- `--action <action>`: Sets the action to perform. `1` = Add, `2` = Del, `3` = Level, `4` = SetPwd, `5` = Test, `6` = EnableType.
- `--user_id <user ID>`: The CMM user ID (optional).
- `--user_name <user name>`: The CMM user name (optional).
- `--user_password <user password>`: The CMM user password (optional).
- `--user_privilege <user privilege>`: The privilege level (optional): Administrator = `4`, Operator = `3`, User = `2`, Callback = `1`, No Access = `15`. No Access is not supported after the AST2600 platform.
- `--account_type <account type>`: Supported account types for CMM management (optional). `0` = SNMP.
- `--account_type_status <account type status>`: Manages account type status (optional). `0` = Disable, `1` = Enable.
- `--ap <authentication protocol>`: The authentication protocol (optional). `0` = MD5, `1` = SHA.
- `--pp <private protocol>`: The private (encryption) protocol (optional). `0` = DES, `1` = AES.
- `--ak <authentication key>`: The authentication key (optional).
- `--pk <private key>`: The private key (optional).

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetCmmUserList --action Add --user_id 3 --user_name NAME3 --user_password PASSWORD3 --user_privilege 3

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetCmmUserList --action Del --user_id 3

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetCmmUserList --action Level --user_id 3 --user_privilege 3

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetCmmUserList --action SetPwd --user_id 3 --user_password PASSWORD3

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetCmmUserList --action Test --user_name NAME3 --user_password PASSWORD3

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetCmmUserList --action EnableType --user_id 3 --account_type SNMP --account_type_status enable --ap 0 --pp DES --ak KEY --pk KEY
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetCmmUserList --action Add --user_id 3 --user_name NAME3 --user_password PASSWORD3 --user_privilege 3
```

## Notes

- The "No Access" user privilege is not supported on platforms after the AST2600 series.
- `--action EnableType` is not supported on platforms before the AST2600 series.
- If the execution Status field for a managed system is SUCCESS, the console output of the managed system will be shown in the Execution Message section of the created log file.
