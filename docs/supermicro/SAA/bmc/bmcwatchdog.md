# BmcWatchDog

Sets a watchdog timer with a corresponding timer action, executes the reset action to start the timer, and retrieves current timer information.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c BmcWatchDog --action Set --timer_action <BmcWatchDog timer actions> --interval <time interval> --countdown <BmcWatchDog count down>
saa -i <IP or host name> -u <username> -p <password> -c BmcWatchDog --action <Info | Reset>
```

### In-Band
```
saa -c BmcWatchDog --action Set --timer_action <BmcWatchDog timer actions> --interval <time interval> --countdown <BmcWatchDog count down>
saa -c BmcWatchDog --action <Info | Reset>
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c BmcWatchDog --action Set --timer_action <BmcWatchDog timer actions> --interval <time interval> --countdown <BmcWatchDog count down>
saa -l <system list file> [-u <username> -p <password>] -c BmcWatchDog --action <Info | Reset>
```

## Options

- `--action <action>`: Required. Sets action: `0` = Set, `1` = Info, `2` = Reset
- `--timer_action <BmcWatchDog timer actions>`: Sets timer action: `0` = NoAction, `1` = HardReset, `2` = PowerDown, `3` = PowerCycle
- `--interval <time interval>`: Sets the watchdog pre-timeout interval in seconds (value 0-255; set to less than 3 counts)
- `--countdown <BmcWatchDog count down>`: Sets the watchdog countdown (value 0-6553)

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p ADMIN -c BmcWatchDog --action set --timer_action 1 --interval 10 --countdown 60
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p ADMIN -c BmcWatchDog --action info
```

### In-Band
```bash
[SAA_HOME]# ./saa -c BmcWatchDog --action set --timer_action 0 --interval 10 --countdown 60
[SAA_HOME]# ./saa -c BmcWatchDog --action set --timer_action 3 --interval 10 --countdown 60
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p ADMIN -c BmcWatchDog --action set --timer_action 2 --interval 10 --countdown 60
[SAA_HOME]# ./saa -l IP_ADDR_RANGE.txt -u ADMIN -p ADMIN -c BmcWatchDog --action reset
```

## Output

```
Item | Value
---- | -----
Watchdog Timer Use | SMS/OS (0x04)
Watchdog Timer Is | Stopped
Watchdog Timer Actions | Hard Reset (0x01)
Pre-timeout interval | 10 seconds
Timer Expiration Flags | 0x10
Initial Countdown | 20 sec
Present Countdown | 0 sec
```

## Notes

- With the `--countdown` option, the value must be set between 0 and 6553.
- With the `--interval` option, the value must be set between 0 and 255. Set the interval to less than 3 counts.
