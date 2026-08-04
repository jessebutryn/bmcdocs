# FindBmcDevices

Finds the available BMC devices within a given network segment, or within the same network (255.255.255.0) as the network interface in the managed system. In-band only.

## Syntax

### In-Band (without --getMACs)
```
saa -c FindBmcDevices [{--start_ip <IP>}{--end_ip <IP>}{--netmask <netmask>}]
```

### In-Band (with --getMACs)
```
saa -c FindBmcDevices --getMACs {--start_ip <IP>}{--end_ip <IP>}{--netmask <netmask>}{--file <filename>} [{--find_user <username>}{--find_password <password>}]
```

## Options

- `--file <file name>` (Optional): The file to write, required with `--getMACs` used.
- `--start_ip <Start IP>` (Optional): Start address of the network to search.
- `--end_ip <End IP>` (Optional): End address of the network to search.
- `--netmask <Netmask>` (Optional): Subnet mask of the network to search.
- `--getMACs` (Optional): Retrieves the MAC addresses of the found BMC devices and writes them to a file.
- `--find_user <Username for find device>` (Optional): Specifies the username for the found BMC devices. Used in conjunction with `--getMACs`.
- `--find_password <Password for find device>` (Optional): Specifies the password for the found BMC devices. Used in conjunction with `--getMACs`.

## Examples

### In-Band
```bash
[SAA_HOME]# ./saa -c FindBmcDevices --start_ip 192.168.34.0 --end_ip 192.168.34.255 --netmask 255.255.255.0

[SAA_HOME]# ./saa -c FindBmcDevices --start_ip 192.168.34.56 --end_ip 192.168.34.200 --netmask 255.255.255.0 --file 123.txt --getMACs
```

## Output

### Without --getMACs
```
Finding available BMC Devices
.....................................................
....................................
10.182.17.5 IPMI
10.182.17.6 X12 AST2600RoT
10.182.17.7 AST2500
...
10.182.17.8 X12 AST2600RoT
10.182.17.9 X12 AST2600RoT
37 BMC device(s) found.
```

### With --getMACs
```
Finding available BMC Devices
.....................................................
..................................................
..................................................
............
3C:EC:EF:E2:57:E3 10.182.17.5 IPMI
3C:EC:EF:33:D4:D6 10.182.17.6 X12 AST2600RoT
AC:1F:6B:D5:8F:E2 10.182.17.7 AST2500
3C:EC:EF:E1:D6:16 10.182.17.8 X13 AST2600RoT
3C:EC:EF:D1:8A:44 10.182.17.9 X12 AST2500
3C:EC:EF:78:19:78 10.182.17.10 M12
3C:EC:EF:09:54:C1 10.182.17.11 X12 AST2600RoT
29 BMC device(s) found 123 was created.
```
