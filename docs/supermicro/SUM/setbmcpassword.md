# SetBmcPassword

Updates the BMC user password.

## Syntax

### OOB and In-Band
```
sum [-i <IP or host name> -u <username> -p <password>] -c SetBmcPassword [--user_id <user ID>] [[--new_password <new password> --confirm_password <confirm password>] | [--pw_file <password file path>]]
```

### Remote In-Band
```
sum -I Remote_INB --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c SetBmcPassword [--user_id <user ID>] [[--new_password <new password> --confirm_password <confirm password>] | [--pw_file <password file path>]] [--remote_sum <remote sum path>]
```

## Options

- `--user_id <user ID>`: Specifies the user ID (default is 2 for Administrator if not specified).
- `--new_password <new password>`: The new password to set.
- `--confirm_password <confirm password>`: Confirmation of the new password.
- `--pw_file <password file path>`: File containing the password information.

## Examples

### OOB with User ID and Password
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBmcPassword --user_id 3 --new_password 12345678 --confirm_password 12345678
```

### OOB with Password File
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBmcPassword --pw_file passwd.txt
```

### In-Band with Password
```
[SUM_HOME]# ./sum -c SetBmcPassword --new_password 12345678 --confirm_password 12345678
```

### In-Band with User ID and Password File
```
[SUM_HOME]# ./sum -c SetBmcPassword --user_id 3 --pw_file passwd.txt
```

### Remote In-Band with User ID and Password File
```
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c SetBmcPassword --user_id 3 --pw_file passwd.txt
```

## Notes

- Without the --user_id option, the user ID is set to 2 (as Administrator) by default.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/setbmcpassword.md