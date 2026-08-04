# KmsManage

Modifies the KMS (Key Management Server) server configurations, uploads TLS certificates, and tests the connection to the KMS server.

## Syntax

### Single System OOB
```
saa -i <IP or host name> -u <username> -p <password> -c KmsManage [--current_password <current password> | --cur_pw_file <current password filename>] [options...]
```

### Single System In-Band
```
saa -c KmsManage [--current_password <current password> | --cur_pw_file <current password filename>] [options...]
```

### Multiple Systems OOB
```
saa -l <system list file> -u <username> -p <password> -c KmsManage [--current_password <current password> | --cur_pw_file <current password filename>] [options...]
```

## Actions

- **GetInfo**: Check the current KMS configurations.
- **Probe**: Test the connection to the specified KMS server.
- **DeleteCA**: Delete a CA certificate.
- **DeleteCert**: Delete a client certificate.
- **DeletePvtKey**: Delete a client private key.
- **DeleteAll**: Delete all certificates and keys.

## Options

- `--current_password <current password>` (Optional): Checks the current BIOS Administrator password.
- `--cur_pw_file <Current Password File>` (Optional): The specified file path to read the current password.
- `--server_ip <server IP address>` (Optional): Enters a KMS server IP address.
- `--second_server_ip <second server IP address>` (Optional): Enters a second KMS server IP address.
- `--port <port>` (Optional): Command optional port(s). The format of `<port>` is "TCP:5696" or "5696". TCP is served as the KMS server port.
- `--time_out <time out>` (Optional): Enters a KMS server connecting time-out.
- `--time_zone <time zone>` (Optional): Enters a correct time zone GMT+.
- `--client_username <client username>` (Optional): Enters a client identity: UserName.
- `--client_password <client password>` (Optional): Enters a client identity: Password.
- `--ca_cert <CA certificate file name>` (Optional): Uploads a CA certificate from the file.
- `--client_cert <client certificate file name>` (Optional): Uploads a client certificate from the file.
- `--pvt_key <private key file name>` (Optional): Uploads a client private key from the file.
- `--pvt_key_pw <private key password>` (Optional): Enters client private key password.
- `--action <action>` (Optional): Sets a KMS manage action (GetInfo, Probe, DeleteCA, DeleteCert, DeletePvtKey, DeleteAll).
- `--reboot` (Optional): Forces the managed system to reboot or power up after operation.
- `--post_complete` (Optional): Waits for the managed system's POST to complete after reboot.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c KmsManage --server_ip 192.168.12.78 --port 5659 --ca_cert ca.crt --client_cert client.crt --pvt_key private.key --action Probe --reboot

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c KmsManage --server_ip 192.168.12.78 --port TCP:5659 --ca_cert ca.crt --client_cert client.crt --pvt_key private.key --action Probe --reboot

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c KmsManage --action DeleteAll --reboot

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c KmsManage --action GetInfo
```

### In-Band
```bash
[SAA_HOME]# ./saa -c KmsManage --server_ip 192.168.12.78 --port 5659 --ca_cert ca.crt --client_cert client.crt --pvt_key private.key --action Probe --reboot

[SAA_HOME]# ./saa -c KmsManage --server_ip 192.168.12.78 --port TCP:5659 --ca_cert ca.crt --client_cert client.crt --pvt_key private.key --action Probe --reboot

[SAA_HOME]# ./saa -c KmsManage --action DeleteAll --reboot

[SAA_HOME]# ./saa -c KmsManage --action GetInfo
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c KmsManage --action GetInfo
```

## Output

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

- To establish a TLS connection and enable the KMS service, valid TLS certificates and a private key must be provided to the KMS server. Use the `--ca_cert`, `--client_cert`, and `--pvt_key` options, or use the `ChangeBiosCfg` command to upload the required files.
- The `--action Probe` option tests the connection to the KMS server and requires a system reboot. Wait for POST to complete after reboot, then use `--action GetInfo` to check the probe status (see "KMS Server Probe Status" in the output above).
- If the execution "Status" field of the managed system shows SUCCESS, the console output will be shown in the "Execution Message" section of the created log file (multiple systems OOB usage).
