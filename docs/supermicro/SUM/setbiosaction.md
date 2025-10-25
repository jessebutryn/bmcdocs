# SetBiosAction

Shows or hides BIOS settings related to BBS (BIOS Boot Specification) priority.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c SetBiosAction --BBS <yes/no> [--reboot]
```

## Options

- `--BBS <yes/no>`: Show (yes) or hide (no) BBS priority related settings.
- `--reboot`: Forces the managed system to reboot after setting the BIOS action.

## Examples

### OOB Show BBS Settings
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c SetBiosAction --BBS yes --reboot
```

### In-Band Hide BBS Settings
```
[SUM_HOME]# ./sum -c SetBiosAction --BBS no --reboot
```

## Notes

- The uploaded configurations will take effect only after the system is rebooted or powered up.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/setbiosaction.md