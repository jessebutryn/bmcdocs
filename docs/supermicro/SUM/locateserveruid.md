# LocateServerUid

Controls the UID (Unit Identifier) of the managed system for easy location in large configurations.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c LocateServerUid --action <action>
```

## Options

- `--action <action>`: Action to perform.
  - `1 = GetStatus`: Get current UID status.
  - `2 = On`: Turn UID on (blue LED illuminated).
  - `3 = Off`: Turn UID off.

## Examples

### OOB Turn UID Off
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c LocateServerUid --action 3
```

### In-Band Get UID Status
```
[SUM_HOME]# ./sum -c LocateServerUid --action GetStatus
```

## Notes

- When the UID is enabled, the blue LED on both the front and rear of the chassis will be illuminated.
- The UID is a unit identifier button for easy system location in large stack configurations.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/locateserveruid.md