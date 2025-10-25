# TimeBmcReset

Sets the BMC reset counter to schedule a BMC reset after a specified delay or immediately.

## Syntax

### OOB and In-Band
```
sum [-i <IP or host name> -u <username> -p <password>] -c TimedBmcReset --delay <BMC reset delay time> | --immediate
```

### Remote In-Band
```
sum -I Remote_INB --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c TimedBmcReset --delay <BMC reset delay time> | --immediate
```

## Options

- `--delay <BMC reset delay time>`: Sets the delay time in minutes before BMC reset.
- `--immediate`: Resets the BMC immediately.

## Examples

### OOB with Delay
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c TimedBmcReset --delay 10
```

### OOB Immediate
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c TimedBmcReset --immediate
```

### In-Band with Delay
```
[SUM_HOME]# ./sum -c TimedBmcReset --delay 20
```

### Remote In-Band with Delay
```
[SUM_HOME]# ./sum -I Remote_INB --oi 192.168.34.56 --ou root --op 111111 -c TimedBmcReset --delay 20
```

## Notes

- This command is not available on X12 and H12 RoT platforms.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/timebmcreset.md