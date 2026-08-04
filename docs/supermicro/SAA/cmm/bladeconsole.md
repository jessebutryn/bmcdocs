# BladeConsole

Launches a remote blade console within CMM based on the specified blade ID and node ID.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c BladeConsole --blade_id <blade ID> --node_id <node ID>
```

## Options

- `--blade_id`: Specifies the blade ID.
- `--node_id`: Specifies the node ID.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c BladeConsole --blade_id A1 --node_id 1
```
