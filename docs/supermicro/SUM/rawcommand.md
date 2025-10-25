# RawCommand

Sends an IPMI raw command to the target system.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c RawCommand --raw <raw command>
```

## Options

- `--raw <raw command>`: The IPMI raw command to send (in hexadecimal format).

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c RawCommand --raw '06 01'
```

```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c RawCommand --raw '0x06 0x01'
```

### In-Band
```
[SUM_HOME]# ./sum -c RawCommand --raw '06 01'
```

```
[SUM_HOME]# ./sum -c RawCommand --raw '0x06 0x01'
```

## Notes

- The raw command must be enclosed in double quotation marks.
- Commands can be specified in hexadecimal format with or without the "0x" prefix.
- The output shows the response from the IPMI command execution.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/rawcommand.md