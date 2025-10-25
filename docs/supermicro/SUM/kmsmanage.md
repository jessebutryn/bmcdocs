# KmsManage

Use the "KmsManage" command to change the KMS server configurations, upload TLS certificates and test the connection to the KMS server. The command only works on the X12/H12 and later platforms. Since SUM 2.9.0, users can save and configure the specific OEM functions for KMS features by using the [--file] option.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c KmsManage
[[--current_password <current password>] | [--cur_pw_file <current password
filename>]] [options…]
```

## Options

| Option | Augment | Description |
|--------|---------|-------------|
| --server_ip | <server IP address> | Enters a KMS server IP address. |
| --second_server_ip | <second server IP> | Enters a second KMS server IP address. |
| --port | <port> | Enters an optional command port(s). The format of <port> is "TCP:5696" or "5696". TCP is for KMS server port. |
| --time_out | <time out> | Enters a KMS server connection time-out. |
| --time_zone | <time zone> | Enters a correct time zone. |
| --client_username | <client username> | Enters a client identity: UserName. |
| --client_password | <client password> | Enters a client identity: Password. |
| --ca_cert | <CA certificate filename> | Uploads a CA certificate from the file. |
| --client_cert | <client certificate filename> | Uploads a client certificate from the file. |
| --pvt_key | <client private key> | Uploads a client private key from the file. |
| --pvt_key_pw | <private key password> | Uploads a client private key from the file. |
| --file | <file name> | When the "--action GetInfo" option is specified, save the OEM configurations to a file. Otherwise, update the OEM settings with the given configuration file. |
| --action | <action> | Sets the KMS management action to:<br>1 = GetInfo: Check the current KMS configurations.<br>2 = Probe: Test the connection to the specified KMS server.<br>3 = DeleteCA: Delete a CA certificate.<br>4 = DeleteCert: Delete a client certificate.<br>5 = DeletePvtKey: Delete a client private key.<br>6 = DeleteAll: Delete all certificates and keys. |
| --reboot | N/A | Forces the managed system to reboot or power up after operation. |
| --post_complete | N/A | Wait for the managed system POST to complete after reboot. |

## Examples

### OOB

```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c KmsManage --server_ip
192.168.12.78 --port 5659 --ca_cert ca.crt --client_cert client.crt --pvt_key
private.key --action Probe --reboot

[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c KmsManage --server_ip
192.168.12.78 --port TCP:5659 --ca_cert ca.crt --client_cert client.crt --
pvt_key private.key --action Probe --reboot

[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c KmsManage --action
DeleteAll --reboot

[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c KmsManage --action
GetInfo
```

### In-band

```
[SUM_HOME]# ./sum -c KmsManage -server_ip 192.168.12.78 --port 5659 --ca_cert
ca.crt --client_cert client.crt --pvt_key private.key --action Probe --reboot

[SUM_HOME]# ./sum -c KmsManage --server_ip 192.168.12.78 --port TCP:5659 --
ca_cert ca.crt --client_cert client.crt --pvt_key private.key --action Probe --
reboot

[SUM_HOME]# ./sum -c KmsManage --action DeleteAll --reboot

[SUM_HOME]# ./sum -c KmsManage --action GetInfo
```

### Console Output

```
Managed system.....................192.168.34.56
 KMS Server IP..................192.168.12.78
 Second KMS Server IP...........192.168.12.79
 KMS TCP Port Number............5696
 KMS Time Out...................3
 KMS TimeZone...................GMT+0
 Client UserName................user123
 Client Password................******
 KMS TLS Certificate
 CA Certificate.................Uploaded
 Client Certifcate..............Uploaded
 Client Private Key.............Uploaded
 KMS Server Probe Status........KMS function works normally
```

## Notes

- To establish a TLS connection and enable the KMS service, it is required to provide the KMS server with the valid TLS certificates and private key. Please use the "--ca_cert", "--client_cert" and "--pvt_key" options or use the "ChangeBiosCfg" command to upload the required files. For details, see E.5.1 File Upload.
- The "--action Probe" option is used to test the connection to the KMS server and requires a system reboot. Wait for the system POST to complete after reboot, and then use the "--action GetInfo" option to check the probe status. See the "KMS Server Probe Status" in the console output example above.