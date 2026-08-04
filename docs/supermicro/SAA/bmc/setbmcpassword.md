# SetBmcPassword

Updates the BMC user password.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SetBmcPassword [--user_id <user ID>] {[--new_password <new password> --confirm_password <confirm password>] | [--pw_file <password file path>]}
```

### In-Band
```
saa -c SetBmcPassword [--user_id <user ID>] {[--new_password <new password> --confirm_password <confirm password>] | [--pw_file <password file path>]}
```

### Remote In-Band
```
saa -I Remote_INB --oi <OS IP address> --ou <OS username> --op <OS password> -c SetBmcPassword [--user_id <user ID>] {[--new_password <new password> --confirm_password <confirm password>] | [--pw_file <password file path>]} [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SetBmcPassword [--user_id <user ID>] {[--new_password <new password> --confirm_password <confirm password>] | [--pw_file <password file path>]}
```

## Options

- `--user_id <user ID>`: Enters the BMC user ID
- `--new_password <new password>`: Sets the new BMC user password
- `--confirm_password <confirms password>`: Confirms the new BMC user password
- `--pw_file <password file>`: The specified file path to read the new BMC user password

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBmcPassword --user_id 3 --new_password 12345678 --confirm_password 12345678
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBmcPassword --pw_file passwd.txt
```

### In-Band
```bash
[SAA_HOME]# ./saa -c SetBmcPassword --new_password 12345678 --confirm_password 12345678
[SAA_HOME]# ./saa -c SetBmcPassword --user_id 3 --pw_file passwd.txt
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c SetBmcPassword --user_id 3 --pw_file passwd.txt
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetBmcPassword
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetBmcPassword --new_password 12345678 --confirm_password 12345678
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetBmcPassword --user_id 3 --pw_file passwd.txt
```

## Notes

- For Multiple Systems OOB usage, the system list file enumerates managed systems row by row. Two formats are supported:
    - Format 1: `BMC_IP_or_HostName New_Password` (requires `-u`/`-p` on the command line)
    - Format 2: `BMC_IP_or_HostName Username Password New_Password` (`-u`/`-p` optional; values in the list file override the command line)
- For Multiple Systems Remote In-Band usage, the same two formats apply. When using `--new_password` or `--pw_file`, `New_Password` can be omitted from the list file and the same new password applies to every system; to set a different password per system, specify `New_Password` per row instead of using `--new_password`/`--pw_file`.
