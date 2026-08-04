# SetBiosPassword

Updates the BIOS Administrator password on the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SetBiosPassword [--current_password <current password> | --cur_pw_file <current password file path>] {--new_password <new password> --confirm_password <confirm password> | --pw_file <password file path>} [--reboot [--post_complete]]
```

### In-Band
```
saa -c SetBiosPassword [--current_password <current password> | --cur_pw_file <current password file path>] {--new_password <new password> --confirm_password <confirm password> | --pw_file <password file path>} [--reboot]
```

### Remote In-Band
```
saa -I Remote_INB --oi <OS IP address> --ou <OS username> --op <OS password> -c SetBiosPassword [--current_password <current password> | --cur_pw_file <current password file path>] {--new_password <new password> --confirm_password <confirm password> | --pw_file <password file path>} [--reboot] [--remote_saa <remote SAA path>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SetBiosPassword [{--new_password <new password> --confirm_password <confirm password> | --pw_file <password file path>} [--current_password <current password> | --cur_pw_file <current password file path>]] [--reboot [--post_complete]]
```

## Options

- `--new_password <new password>`: Sets the new BIOS Administrator password
- `--confirm_password <confirm password>`: Confirms the new BIOS Administrator password
- `--current_password <current password>`: Checks the current BIOS Administrator password
- `--reboot`: Forces the managed system to reboot or power up after operation
- `--pw_file <Password File>`: The specified file path to read the new password
- `--post_complete`: Waits for the managed system's POST to complete after reboot
- `--cur_pw_file <Current Password File>`: The specified file path to read the current password

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBiosPassword --new_password 123456 --confirm_password 123456 --current_password 654321 --reboot
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBiosPassword --pw_file passwd.txt --reboot
```

### In-Band
```bash
[SAA_HOME]# ./saa -c SetBiosPassword --new_password 123456 --confirm_password 123456 --reboot
[SAA_HOME]# ./saa -c SetBiosPassword --pw_file passwd.txt --cur_file cur_passwd.txt --reboot
```

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c SetBiosPassword --new_password 123456 --confirm_password 123456 --reboot --remote_saa /root/saa
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c SetBiosPassword --pw_file passwd.txt --cur_file cur_passwd.txt --reboot --remote_saa /root/saa
```

### Multiple Systems OOB (per-system passwords via system list file)
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetBiosPassword
```

### Multiple Systems OOB (same new/current password for every system)
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetBiosPassword --new_password 12345678 --confirm_password 12345678 --current_password 654321
```

## Notes

- For Multiple Systems OOB usage, the system list file format is fixed for this command. Both `New_BIOS_Password` and `Current_Password` fields are REQUIRED; if the managed system has no BIOS Administrator password installed, fill the field with an empty value. Two formats are supported:
    - Format 1: `BMC_IP_or_HostName New_BIOS_Password Current_BIOS_Password` (requires `-u` and `-p` on the command line)
    - Format 2: `BMC_IP_or_HostName Username Password New_BIOS_Password Current_BIOS_Password` (`-u`/`-p` optional on the command line; if present in the list file, they override the command-line options)
- For Multiple Systems Remote In-Band usage, two formats are supported:
    - Format 1: `OS_IP_or_HostName OS_Username OS_Password New_BIOS_Password Current_BIOS_Password`
    - Format 2: `OS_IP_or_HostName OS_Username OS_PrivateKey OS_Privatekey_Password New_BIOS_Password Current_BIOS_Password`
- If `--new_password`/`--pw_file` or `--current_password`/`--cur_pw_file` are specified on the command line, those values override the corresponding per-system values in the system list file.
