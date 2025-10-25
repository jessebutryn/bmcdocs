# SetCmmPassword

Updates the CMM user password.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c SetCmmPassword [--user_id <user ID>] [[--new_password <new password> --confirm_password <confirm password>] | [--pw_file <password file path>]]
```

## Options

- `--user_id <user ID>`: Specifies the user ID (default is 2 for Administrator if not specified).
- `--new_password <new password>`: The new password to set.
- `--confirm_password <confirm password>`: Confirmation of the new password.
- `--pw_file <password file path>`: File containing the password information.

## Examples

### OOB with User ID and Password
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetCmmPassword --user_id 3 --new_password 12345678 --confirm_password 12345678
```

### OOB with Password File
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetCmmPassword --pw_file passwd.txt
```

### In-Band with Password
```
[SUM_HOME]# ./sum -c SetCmmPassword --new_password 12345678 --confirm_password 12345678
```

### In-Band with User ID and Password File
```
[SUM_HOME]# ./sum -c SetCmmPassword --user_id 3 --pw_file passwd.txt
```

## Notes

- Without the --user_id option, the user ID is set to 2 (as Administrator) by default.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/setcmmpassword.md