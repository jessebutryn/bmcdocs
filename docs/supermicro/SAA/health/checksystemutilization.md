# CheckSystemUtilization

Checks the device utilization status for the managed system (OOB only). Requires the TAS thin agent to be installed and the OS of the managed system to be booted, in order to collect real-time device utilization.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c CheckSystemUtilization
```

### Multiple Systems OOB
```
saa -l <system list file> -u <username> -p <password> -c CheckSystemUtilization
```

## Options

None

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CheckSystemUtilization
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c CheckSystemUtilization
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

If the execution "Status" field for a managed system is SUCCESS, the utilization status of the managed system is shown in the "Execution Message" section in the created log file.

## Output

```
Time
====
 Last Sample Time: 2014-05-16_17:16:02
OS
==
 OS Name: RedHatEnterpriseServer
 OS Version: 6.4 x86_64
CPU
===
 CPU Utilization: 2.74 %
Memory
======
 Memory Utilization: 8 %
LSI(1)
======
 HDD Name: /dev/sdb
 Slot number: 1
 SMART Status: Ok
HDD(1)
======
 HDD name: /dev/sda
 SMART Status: Ok
 Serial number: Z2AABXL3
 Total Partitions: 2
 [Partition(1)]
 Partition Name: /dev/sda1
 Utilization: N/A
 Used Space: N/A
 Total Space: 17.58 GB
 [Partition(2)]
 Partition Name: /dev/sda2
 Utilization: 22.01 %
 Used Space: 3.62 GB
 Total Space: 17.30 GB
RSTe(1)
======
 Volume name: /dev/md126
 Controller name: Intel RSTe
 Numbers of Drives: 2
 [HDD(1)]
 HDD name: /dev/sdc
 SMART Status: Ok
 [HDD(2)]
 HDD name: /dev/sdd
 SMART Status: Ok
Network
=======
 Total Devices: 2
 [NIC(1)]
 Device Name: eth0
 Utilization: <1 %
 Status: up
 [NIC(2)]
 Device Name: eth1
 Utilization: 0 %
 Status: down
```

## Notes

- This command requires a TAS agent to collect the system statuses.
- If a TAS agent is not installed on the managed system, the system statuses are shown as N/A.
- The OS of the managed system must be booted for the TAS agent to collect real-time device utilization.
- RAID device types LSI, RSTe, and NVMe are shown only if they have been installed on the host machine.
- When an RSTe device is installed on the host machine, normal Hard Disk (HDD) type information is not displayed.
