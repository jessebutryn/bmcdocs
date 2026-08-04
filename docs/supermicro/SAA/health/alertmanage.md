# AlertManage

Gets different types of alert messages received on the managed system, and can send a test alert. Alert messages are received by the AlertServer application (in the `GO_SNMP` subfolder of the SAA package), which runs a basic HTTPS server and SNMP listener for SNMPv1, SNMPv3, and Redfish alerts, and writes them to a SQLite database that `AlertManage` reads. The `.saarc` file configures the path to this database.

## Syntax

### In-Band (list messages)
```
saa -c AlertManage --action listmessage --message_type <List of message type> [--after <datetime>] [--before <datetime>] [--ip <Sender IP>] [--page <Page>] [--limit <limit>]
```

### OOB / In-Band (send test alert)
```
saa <-i <IP or host name> | -I Redfish_HI> -u <username> -p <password> -c AlertManage --action sendTest
```

## Options

- `--action <action>`: Sets action:
    - `1` = listMessage
    - `2` = sendTest
- `--message_type <List of message type>`:
    - `1` = nmpv1 (SNMPv1)
    - `3` = snmpv3
    - `4` = redfishAlert
- `--after <datetime>`: (Optional) Queries trap messages after the specified time.
- `--before <datetime>`: (Optional) Queries trap messages before the specified time.
- `--ip <Sender IP>`: (Optional) Queries trap messages from the specified IP address.
- `--page <Page>`: (Optional) Sets the page number; the default value is the first page.
- `--limit <limit>`: (Optional) Sets the quantity of data per page, range 10 to 100; the default value is twenty.

## Examples

### Listing Messages
```bash
[SAA_HOME]# ./saa -c AlertManage --action listMessage --message_type Snmpv1
```

### Querying Messages
```bash
# Messages after a certain time
[SAA_HOME]# ./saa -c AlertManage --action listmessage --message_type snmpv1 --after "2022-12-09 19:48:36"

# Messages before a certain time
[SAA_HOME]# ./saa -c AlertManage --action listmessage --message_type snmpv1 --before "2022-12-09 19:48:36"

# Messages between two times
[SAA_HOME]# ./saa -c AlertManage --action listmessage --message_type snmpv1 --after "2022-12-08 19:48:36" --before "2022-12-09 19:48:36"

# Messages from a specific sender IP
[SAA_HOME]# ./saa -c AlertManage --action listmessage --message_type snmpv1 --ip 192.168.34.56

# Paging: 10 messages per page, page 3
[SAA_HOME]# ./saa -c AlertManage --action listmessage --message_type snmpv1 --limit 10 --page 3

# Combined filters
[SAA_HOME]# ./saa -c AlertManage --action listmessage --message_type 1 --ip 192.168.34.56 --after "2023-1-1 00:00:00" --before "2023-1-1 14:00:00" --limit 10 --page 3
```

### Sending a Test Alert (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c AlertManage --action sendTest
```

### Sending a Test Alert (In-Band)
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p ADMIN -c AlertManage --action sendTest
```

## Output

```
[Notice]
 No matching results with SnmpV1 message
 #The searching criteria:
 #IP : 192.168.34.56
 #timeafter : 2023-1-1 00:00:00
 #timebefore : 2023-1-1 14:00:00
[Page Info]
#Total 0 records
```

When using `AlertManage`, every search option value is echoed under the notice title, and Page Info lists the number of pages that can be navigated to.

## Notes

- To receive alert messages, configure the server IP location through BMC, either with the SAA `SetBmcCfg` command or via the BMC web page (Configuration/Notifications > Alerts tab).
- The `snmp.env` file in the `GO_SNMP` folder configures AlertServer, including SNMPv3 UserName, AuthenticationProtocol (MD5, SHA, SHA224, SHA256, SHA384, SHA512), AuthenticationPassphrase, PrivacyProtocol (DES, AES, AES192, AES256, AES192C, AES256C), PrivacyPassphrase, `db_path` (default `default.db`), `server_cert`, `server_key`, and `log_level` (1 = no log, 2 = simple log, 3 = complete log).
- The default values for `--limit` and `--page` are 20 and 1, respectively.
- The `sendTest` action only supports Redfish Host Interface, OOB, and multiple-systems OOB usage.
