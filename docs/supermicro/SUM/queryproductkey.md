# QueryProductKey

Queries the node product keys activated in the managed system.

## Syntax

```
sum [[-i <IP or host name> | -I <Redfish_HI>] -u <username> -p <password>] -c QueryProductKey
```

## Examples

**OOB:**
```bash
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c QueryProductKey
```

**In-Band:**
```bash
[SUM_HOME]# ./sum -c QueryProductKey
```

## Output

The console output contains activated node product keys with details like key name, invoice, creation date, and total number of keys.

Example output:
```
SFT-OOB-LIC
SFT-DCMS-SINGLE , invoice: X8800693687A, creation date: 2019/12/03
SFT-SPM-LIC , invoice: X8800693688A, creation date: 2019/12/04
SFT-DCMS-SVC-KEY, invoice: X8800693689A, creation date: 2019/12/04
Number of product keys: 4
```