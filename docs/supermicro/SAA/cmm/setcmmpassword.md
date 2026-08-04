# SetCmmPassword

Updates the CMM user password.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SetCmmPassword [--user_id <user ID>] {[--new_password <new password> --confirm_password <confirm password>] | [--pw_file <password file path>]}
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SetCmmPassword [--user_id <user ID>] {[--new_password <new password> --confirm_password <confirm password>] | [--pw_file <password file path>]}
```

## Options

- `--user_id <user ID>`: Enters the CMM user ID.
- `--new_password <new password>`: Sets the new CMM user password.
- `--confirm_password <confirm password>`: Confirms the new CMM user password.
- `--pw_file <password file>`: The specified file path to read the new CMM user password.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetCmmPassword --user_id 3 --new_password 12345678 --confirm_password 12345678
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetCmmPassword --pw_file passwd.txt
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetCmmPassword --new_password 12345678 --confirm_password 12345678
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetCmmPassword --user_id 3 --pw_file passwd.txt
```

## Notes

- Without the `--user_id` option, the user ID is set to 2 (Administrator) by default.
