# SetBiosPassword

Updates the BIOS Administrator password.

## Syntax

### OOB and In-Band
```
sum [-i <IP or host name> -u <username> -p <password>] -c SetBiosPassword [[--current_password <current password>] | [--cur_pw_file <current password file path>]] [[--new_password <new password> --confirm_password <confirm password>] | [--pw_file <password file path>]] [--reboot]
```

### Remote In-Band
```
sum -I Remote_INB --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c SetBiosPassword [[--current_password <current password>] | [--cur_pw_file <current password file path>]] [[--new_password <new password> --confirm_password <confirm password>] | [--pw_file <password file path>]] [--reboot] [--remote_sum <remote sum path>]
```

## Options

- `--current_password <current password>`: Current BIOS password.
- `--cur_pw_file <current password file path>`: File containing the current BIOS password.
- `--new_password <new password>`: New BIOS password to set.
- `--confirm_password <confirm password>`: Confirmation of the new BIOS password.
- `--pw_file <password file path>`: File containing the new password information.
- `--cur_file <current password file>`: File containing the current password (in-band only).
- `--reboot`: Forces the managed system to reboot after setting the password.

## Examples

### OOB with Passwords
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBiosPassword --new_password 123456 --confirm_password 123456 --current_password 654321 --reboot
```

### OOB with Password File
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBiosPassword --pw_file passwd.txt --reboot
```

### In-Band with Passwords
```
[SUM_HOME]# ./sum -c SetBiosPassword --new_password 123456 --confirm_password 123456 --reboot
```

### In-Band with Password Files
```
[SUM_HOME]# ./sum -c SetBiosPassword --pw_file passwd.txt --cur_file cur_passwd.txt --reboot
```

### Remote In-Band with Passwords
```
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c SetBiosPassword --new_password 123456 --confirm_password 123456 --reboot --remote_sum /root/sum
```

### Remote In-Band with Password Files
```
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c SetBiosPassword --pw_file passwd.txt --cur_file cur_passwd.txt --reboot --remote_sum /root/sum
```

## Notes

- The command requires either the current password or a file containing it to change the BIOS password.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/setbiospassword.md