# SetBmcUserList

Manages the BMC user list on the managed system.

## Syntax

### Add User (OOB)
```
sum -i <IP or host name> -u <username> -p <password> -c SetBmcUserList --action add --user_id <userid> --user_name <username> --user_password <userpassword> --user_privilege <userprivilege> [--user_status <status>] [--manage_account_type <type:status>]
```

### Add User (In-Band Redfish_HI)
```
sum [-I Redfish_HI -u <username> -p <password>] -c SetBmcUserList --action add --user_id <userid> --user_name <username> --user_password <userpassword> --user_privilege <userprivilege> [--user_status <status>] [--manage_account_type <type:status>]
```

### Other Actions (OOB)
```
sum [-i <IP or host name> -u <username> -p <password>] -c SetBmcUserList --action <action> --user_id <userid> [--user_name <username>] [--user_password <userpassword>] [--user_privilege <userprivilege>]
```

### Test User Login
```
sum {-i <IP or host name> | -I Redfish_HI} -u <username> -p <password> -c SetBmcUserList --action Test --user_name <username> --user_password <userpassword>
```

### Enable User Type
```
sum {-i <IP or host name> | -I Redfish_HI} -u <username> -p <password> -c SetBmcUserList --action EnableType --user_id <userid> {--account_type <type> --account_type_status <status> | --manage_account_type <type:status>} [--ap <protocol> --pp <protocol> --ak <key> --pk <key>]
```

### Enable User Account
```
sum {-i <IP or host name> | -I Redfish_HI} -u <username> -p <password> -c SetBmcUserList --action EnableAccount --user_id <userid> --user_status <status>
```

### In-Band Actions
```
sum -c SetBmcUserList --action <action_number> [options…]
```

## Actions

- `add` or `1`: Add a new BMC user.
- `Del` or `2`: Delete a BMC user.
- `Level` or `3`: Change BMC user privilege.
- `SetPwd` or `4`: Change BMC user password.
- `Test` or `5`: Test BMC user login.
- `EnableType` or `6`: Enable BMC user type.
- `EnableAccount` or `7`: Enable BMC user status.

## Options

- `--user_id <userid>`: User ID number.
- `--user_name <username>`: Username.
- `--user_password <userpassword>`: User password.
- `--user_privilege <userprivilege>`: User privilege level.
- `--user_status <status>`: User status (Enable/Disable).
- `--manage_account_type <type:status>`: Account type management (e.g., SNMP:Enable,Redfish:Disable).
- `--account_type <type>`: Account type (e.g., SNMP).
- `--account_type_status <status>`: Account type status (Enable/Disable).
- `--ap <protocol>`: Authentication protocol.
- `--pp <protocol>`: Privacy protocol.
- `--ak <key>`: Authentication key.
- `--pk <key>`: Privacy key.

## Examples

### OOB Add User
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBmcUserList --action add --user_id 3 --user_name NAME3 --user_password PASSWORD3 --user_privilege 3 --user_status Disable --manage_account_type SNMP:Enable,Redfish:Disable --ap SHA --pp DES --ak AKEY3 --pk PKEY3
```

### OOB Delete User
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBmcUserList --action Del --user_id 3
```

### OOB Change Privilege
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBmcUserList --action Level --user_privilege 3
```

### OOB Set Password
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBmcUserList --action SetPwd --user_id 3 --user_password PASSWORD3
```

### OOB Test Login
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBmcUserList --action Test --user_name NAME3 --user_password PASSWORD3
```

### OOB Enable Type
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBmcUserList --action EnableType --user_id 3 --account_type SNMP --account_type_status Enable --ap SHA --pp DES --ak AKEY3 --pk PKEY3
```

### OOB Enable Account
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBmcUserList --action EnableAccount --user_id 3 --user_status Disable
```

### In-Band Add User
```
[SUM_HOME]# ./sum -c SetBmcUserList --action 1 --user_id 3 --user_name NAME3 --user_password PASSWORD3 --user_privilege 3
```

### In-Band Redfish_HI Add User
```
[SUM_HOME]# ./sum -I Redfish_HI -u ADMIN -p PASSWORD -c SetBmcUserList –action 1 --user_id 3 --user_name NAME3 --user_password PASSWORD3 --user_privilege 3 --user_status Disable --manage_account_type SNMP:Enable,Redfish:Disable --ap SHA --pp DES --ak AKEY3 --pk PKEY3
```

### In-Band Delete User
```
[SUM_HOME]# ./sum -c SetBmcUserList --action 2 --user_id 3
```

### In-Band Change Privilege
```
[SUM_HOME]# ./sum -c SetBmcUserList --action 3 --user_id 3 --user_privilege 3
```

### In-Band Set Password
```
[SUM_HOME]# ./sum -c SetBmcUserList --action 4 --user_id 3 --user_password PASSWORD3
```

### In-Band Redfish_HI Test Login
```
[SUM_HOME]# ./sum -I Redfish_HI -u ADMIN -p PASSWORD -c SetBmcUserList --action 5 --user_name NAME3 --user_password PASSWORD3
```

### In-Band Redfish_HI Enable Type
```
[SUM_HOME]# ./sum -I Redfish_HI -u ADMIN -p PASSWORD -c SetBmcUserList --action 6 --user_id 3 --account_type SNMP --account_type_status Enable --ap SHA --pp DES --ak AKEY3 --pk PKEY3
```

### In-Band Redfish_HI Enable Account
```
[SUM_HOME]# ./sum -I Redfish_HI -u ADMIN -p PASSWORD -c SetBmcUserList --action 7 --user_id 3 --user_status Disable
```

## Notes

- "No Access," a user privilege, is not supported on platforms after X11/H11.
- The "--action EnableType" and "--action EnableAccount" is not supported on platforms before X12/H12.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/setbmcuserlist.md