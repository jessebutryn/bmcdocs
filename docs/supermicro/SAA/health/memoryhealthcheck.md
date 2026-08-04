# MemoryHealthCheck

Accesses the BIOS function to check the memory health of the managed system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c MemoryHealthCheck {--action <action>} [--reboot [--post_complete]]
```

### In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c MemoryHealthCheck {--action <action>} [--reboot]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c MemoryHealthCheck {--action <action>} [--reboot [--post_complete]]
```

## Options

- `--action <action>`: Sets action:
    - `1` = GetCurrentStatus
    - `2` = Persistent
    - `3` = Enable
    - `4` = Disable
- `--reboot`: (Optional) Forces the managed system to reboot or power up after the operation.
- `--post_complete`: (Optional) Waits for the managed system POST to complete after rebooting.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c MemoryHealthCheck --action GetCurrentStatus

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c MemoryHealthCheck --action Persistent --reboot --post_complete
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c MemoryHealthCheck --action Enable --reboot
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c MemoryHealthCheck --action Persistent --reboot --post_complete
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

If the execution "Status" field for a managed system is SUCCESS, the utilization status of the managed system is shown in the "Execution Message" section in the created log file.

## Output

### GetCurrentStatus
```
The current memory health checking is Disabled
```

### Persistent with reboot
```
The memory health checking is set to Persistent.
Status: The managed system 192.168.34.56 is rebooting.
.........................Done
Status: The managed system 192.168.34.56 is waiting for POST complete
.........................
..................................................
..................................................
..................................................
..................................................
..................................................
..................................................
..................................................
...................
Status: The managed system 192.168.34.56 is POST completed
Status: Getting event logs from 192.168.34.56.
ID| Time Stamp | Sensor Number | Sensor Type | Description
18| 01/20/2022 08:33:10 | #0FF (System Firmware Progress) | System Firmware Progress | Progress: CPU 1 Advanced Memory Test finished
17| 01/20/2022 08:32:13 | #0FF (System Firmware Progress) | System Firmware Progress | Progress: CPU 1 Advanced Memory Test started
```

## Notes

- This command is only available on X13 and later platforms.
