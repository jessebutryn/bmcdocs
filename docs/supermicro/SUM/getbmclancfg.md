# GetBmcLANCfg

Use the "GetBmcLANCfg" command to execute SUM to get the current BMC LAN settings from the managed system and save them in the BMCLANCfg.xml file.

## Syntax

```
sum [[-i <IP or host name> | -I Redfish_HI] -u <username> -p <password>] -c
GetBmcLANCfg --file <BMCLANCfg.xml> [--overwrite]
```

## Options

| Option | Augment | Description |
|--------|---------|-------------|
| --file | <BMCLANCfg.xml> | Save the BMC LAN configuration to the specified XML file. |
| --overwrite | N/A | Overwrite the file if it already exists. |

## Examples

### OOB

```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetBmcLANCfg --file
BMCCfg.xml --overwrite
```

### In-band

```
[SUM_HOME]# ./sum -c GetBmcLANCfg --file BMCLANCfg.xml --overwrite

[SUM_HOME]# ./sum -I Redfish_HI -u ADMIN -p PASSWORD -c GetBmcLANCfg --file
BMCLANCfg.xml --overwrite
```

## Notes

- The received tables/elements might not be identical between two managed systems. Only supported tables/elements for the managed system will be received.
- For in-band and OOB usages, note that the file formats for getting BMC LAN settings may be different. Be careful not to misuse them.