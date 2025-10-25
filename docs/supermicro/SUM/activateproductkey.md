# ActivateProductKey

Activates a node product key for the managed system.

## Syntax

```
sum [[-i <IP or host name> | -I Redfish_HI] -u <username> -p <password>] -c ActivateProductKey [--key <nodeproductkey> | --key_file <file name>]
```

## Options

- `--key <nodeproductkey>`: The node product key to activate (can be in plain text or JSON format)
- `--key_file <file name>`: File containing the node product key

## Examples

**OOB:**
```bash
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c ActivateProductKey --key 1111-1111-1111-1111-1111-1111
```

**In-Band:**
```bash
[SUM_HOME]# ./sum -c ActivateProductKey --key 1111-1111-1111-1111-1111-1111
```

**With JSON key:**
```bash
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c ActivateProductKey --key '{"ProductKey":{"Node":{"LicenseID":"1","LicenseName":"SFT-OOBLIC","CreateDate":"20200409"},"Signature":"..."}}'
```

**With key file:**
```bash
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c ActivateProductKey --key_file mymacs.txt.key
```

## Notes

- A node product key in JSON format must be put in single quotation marks.
- When activating a key in JSON format in Windows, the JSON key string cannot contain any spaces.