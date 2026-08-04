# BmcIPv6StaticRouteManage

Manages the BMC IPv6 static route: gets or sets the static route status to Enabled/Disabled, sets a static route, or clears static route settings.

- Use `--action GetInfo` to retrieve the settings of the static route.
- Use `--action Enable` or `--action Disable` to change the status of the static route.
- Use `--action SetStaticRoute` with `--ipv6_ip`, `--ipv6_prefix_value`, `--ipv6_prefix_len`, and `--router_id` to set the IPv6 static route.
- Use `--action Clear` with `--router_id` to clear the IPv6 static route settings.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c BmcIPv6StaticRouteManage --action <action> [--router_id <Router ID> [--ipv6_ip <IPv6 IP> --ipv6_prefix_value <IPv6 prefix value> --ipv6_prefix_len <IPv6 prefix length>]]
```

### In-Band
```
saa -c BmcIPv6StaticRouteManage --action <action> [--router_id <Router ID> [--ipv6_ip <IPv6 IP> --ipv6_prefix_value <IPv6 prefix value> --ipv6_prefix_len <IPv6 prefix length>]]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c BmcIPv6StaticRouteManage --action <action> [--router_id <Router ID> [--ipv6_ip <IPv6 IP> --ipv6_prefix_value <IPv6 prefix value> --ipv6_prefix_len <IPv6 prefix length>]]
```

## Options

- `--action <action>`: Required. Sets action: `1` = GetInfo, `2` = Enable, `3` = Disable, `4` = SetStaticRoute, `5` = Clear
- `--ipv6_ip <IPv6 IP>`: Specifies the IPv6 IP address for configuration
- `--ipv6_prefix_value <IPv6 prefix value>`: Specifies the IPv6 prefix value for configuration
- `--ipv6_prefix_len <IPv6 prefix length>`: Specifies the IPv6 prefix length for configuration
- `--router_id <Router ID>`: Specifies an IPv6 router for configuration; the value is `1` or `2`

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c BmcIPv6StaticRouteManage --action GetInfo
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c BmcIPv6StaticRouteManage --action Enable
```

### In-Band
```bash
[SAA_HOME]# ./saa -c BmcIPv6StaticRouteManage --action SetStaticRoute --ipv6_ip 1111:2222::CCCC --ipv6_prefix_value AAAA:BBBB:: --ipv6_prefix_len 64 --router_id 2
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c BmcIPv6StaticRouteManage --action Clear --router_id 2
```

## Output

```
Managed system................localhost
Status........................Disabled
 Route 1
 Prefix to Route.......ABCD:0000:0000:0000:0000:0000:0000:0000/64
 Router Address........ABCD:0000:0000:0000:0000:0000:1234:5678
 Route 2
 Prefix to Route.......0000:0000:0000:0000:0000:0000:0000:0000/255
 Router Address........0000:0000:0000:0000:0000:0000:0000:0000
```

## Notes

- If the execution "Status" field of the managed system shows SUCCESS, the console output of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
