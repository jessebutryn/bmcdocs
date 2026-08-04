# SetKcsPriv

Sets the BMC KCS (Keyboard Controller Style) privilege level. This command only supports OOB usage.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c SetKcsPriv {--priv_level <KCS privilege level>}
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c SetKcsPriv {--priv_level <KCS privilege level>}
```

## Options

- `--priv_level <KCS privilege level>`: Sets the KCS privilege level: `1` = Call Back, `2` = User, `3` = Operator, `4` = Administrator

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetKcsPriv --priv_level 'Call Back'
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetKcsPriv --priv_level 1
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetKcsPriv --priv_level 'Call Back'
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c SetKcsPriv --priv_level 1
```

## Notes

- SAA only supports the following KCS privileges: Call Back, User, Operator, and Administrator.
- This command only supports OOB usage.
- The BMC KCS privilege can be set through a numeric ID or a name.
