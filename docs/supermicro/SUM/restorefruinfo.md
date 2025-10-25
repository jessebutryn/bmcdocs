# RestoreFruInfo

Restores FRU (Field Replaceable Unit) information on the managed system.

## Syntax

```
sum [-i <IP or host name>] -u <username> -p <password> -c RestoreFruInfo --file <filename>
```

## Options

- `--file <filename>`: Path to the FRU information file to restore.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c RestoreFruInfo --file dumpedFile
```

### In-Band
```
[SUM_HOME]# ./sum -c RestoreFruInfo --file dumpedFile
```

## Notes

- The FRU information file should be obtained using the GetFruInfo command.
- The command restores FRU information including manufacturing date, board information, and product details.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/restorefruinfo.md