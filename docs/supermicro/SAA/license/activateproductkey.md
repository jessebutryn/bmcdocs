# ActivateProductKey

Activates the managed system using a node product key obtained from Supermicro, either as a direct key value or from a key file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c ActivateProductKey {--key <nodeproductkey> | --key_file <file name>}
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c ActivateProductKey {--key <nodeproductkey> | --key_file <file name>}
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c ActivateProductKey
```

## Options

- `--key <node product key value>`: (Optional) Uses the node product key to activate the managed system.
- `--key_file <file name>`: (Optional) Uses the node product key file to activate the managed system.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ActivateProductKey --key 1111-1111-1111-1111-1111-1111

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ActivateProductKey --key '{"ProductKey":{"Node":{"LicenseID":"1","LicenseName":"SFT-OOBLIC","CreateDate":"20200409"},"Signature":"111111111111111111112222222222222233333333333333ababababababababababababbabcdcdcdcdcdcdccdcdcddcdefefefefefefefeefefefefghghghghghghghghghgh"}}'

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ActivateProductKey --key_file mymacs.txt.key
```

### In-Band
```bash
[SAA_HOME]# ./saa -c ActivateProductKey --key 1111-1111-1111-1111-1111-1111

[SAA_HOME]# ./saa -c ActivateProductKey --key '{"ProductKey":{"Node":{"LicenseID":"1","LicenseName":"SFT-OOBLIC","CreateDate":"20200409"},"Signature":"111111111111111111112222222222222233333333333333ababababababababababababbabcdcdcdcdcdcdccdcdcddcdefefefefefefefeefefefefghghghghghghghghghgh"}}'

[SAA_HOME]# ./saa -c ActivateProductKey --key_file mymacs.txt.key

[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c ActivateProductKey --key 1111-1111-1111-1111-1111-1111

[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c ActivateProductKey --key_file mymacs.txt.key
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ActivateProductKey

[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ActivateProductKey --key_file mymacs.text.key
```

`SList.txt`:
```
192.168.34.56 1111-1111-1111-1111-1111-1111
192.168.34.57 ADMIN1 PASSWORD1 2222-2222-2222-2222-2222-2222
192.168.34.58 {"ProductKey":{"Node":{"LicenseID":"1","LicenseName":"SFT-OOBLIC","CreateDate":"20200409"},"Signature":"11111111111111111111222222222222222333333333333333ababababababababababababbabcdcdcdcdcdcdccdcdcddcdefefefefefefefeefefefefghghghghghghghghghgh"}}
```

For the first managed system (192.168.34.56), SAA applies `-u ADMIN` and `-p PASSWORD` from the command line with the node product key from the list. For the second managed system (192.168.34.57), SAA instead uses the username, password, and node product key given in that row of the list file. Both managed systems are activated concurrently.

## Notes

- A node product key in JSON format must be enclosed in single quotation marks.
- When activating a JSON-format key on Windows, the JSON key string cannot contain any spaces.
- For details on the format of a product key file (e.g. `mymacs.txt.key`), see the "Getting Node Product Keys from Supermicro" section of the guide and follow the instructions on the website to load the device driver.
- In a system list file, per-row username/password/key values override the `-u`/`-p` command-line options.
