# RmcpManage

Gets RMCP information and manages an RMCP service port.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c RmcpManage --action <GetInfo|Enable|Disable> [--port <port>]
```

### In-Band
```
saa -c RmcpManage --action <GetInfo|Enable|Disable> [--port <port>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c RmcpManage --action <GetInfo|Enable|Disable> [--port <port>]
```

## Options

- `--action <action>`: Required. Sets RMCP status: `1` = GetInfo, `2` = Enable, `3` = Disable
- `--port <port>`: Optional port(s), in the format `RMCP:623` or `623`. Supported port: RMCP (for the RMCP service port)

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c RmcpManage --action GetInfo
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c RmcpManage --action Enable --port RMCP:623
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c RmcpManage --action Enable --port 623
```

### In-Band
```bash
[SAA_HOME]# ./saa -c RmcpManage --action Enable --port RMCP:623
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c RmcpManage --action Enable --port RMCP:623
```

## Output

```
Managed system................192.168.34.56
 RMCP Status...............Enable
 RMCP Port.................623
```
