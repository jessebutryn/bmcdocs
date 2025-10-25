# UpdatePsu

## Description

Use the "UpdatePsu" command with a signed PSU firmware image requested by OEM and the PSU slave address to run SUM to update the managed system.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c UpdatePsu --file <filename> --address <PSU slave address>
```

## Options

- `--file <filename>`: Specifies the signed PSU firmware image file.
- `--address <PSU slave address>`: Specifies the slave address of the PSU to update.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c UpdatePsu --file Supermicro_PSU.x0 --address 0x80
```

### In-Band
```
[SUM_HOME]# ./sum -c UpdatePsu --file Supermicro_PSU.x0 --address 0x80
```

## Notes

- During PSU firmware updating process, the updated PSU will be powered off. To use this command, the system needs to connect to at least two PSUs.
- Slave address of the PSU that needs to be updated can be found by executing the "GetPsuInfo" command.
- The updated PSU will be rebooted automatically when firmware update completes.
- PSU updated on the system with LCMC is only supported on X11 Intel® Xeon® Scalable Processors with Intel® C620 Series Chipsets and later platforms.
