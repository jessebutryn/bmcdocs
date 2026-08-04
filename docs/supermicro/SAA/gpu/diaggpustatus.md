# DiagGpuStatus

Diagnoses AMD Instinct MI250 GPU system status, including power rail status per GPU.

## Syntax

### Single System

#### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c DiagGpuStatus [--dev_id <dev_id_list>]
```

#### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c DiagGpuStatus [--dev_id <dev_id_list>]
```

### Multiple Systems

#### OOB
```
saa -l <system list file> [-u <username> -p <password>] -c DiagGpuStatus [--dev_id <dev_id_list>]
```

## Options

- `--dev_id <Device ID List>` (Optional): The device ID list of GPUs on the managed system.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c DiagGpuStatus
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c DiagGpuStatus --dev_id 2,4,8
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c DiagGpuStatus
```

## Output

### All GPUs
```
AMD INSTINCT MI250
===================
[GPU(1)]
 Serial Number..............PCB012345671
 Power rails Status.........OK
[GPU(2)]
 Serial Number..............PCB012345672
 Power rails Status.........OK
[GPU(3)]
 Serial Number..............PCB012345673
 Power rails Status.........OK
[GPU(4)]
 Serial Number..............PCB012345674
 Power rails Status.........OK
[GPU(5)]
 Serial Number..............PCB012345675
 Power rails Status.........OK
[GPU(6)]
 Serial Number..............PCB012345676
 Power rails Status.........OK
[GPU(7)]
 Serial Number..............PCB012345677
 Power rails Status.........OK
[GPU(8)]
 Serial Number..............PCB012345678
 Power rails Status.........OK
```

### Filtered by --dev_id
```
AMD INSTINCT MI250
===================
[GPU(2)]
 Serial Number..............PCB012345672
 Power rails Status.........OK
[GPU(4)]
 Serial Number..............PCB012345674
 Power rails Status.........OK
[GPU(8)]
 Serial Number..............PCB012345678
 Power rails Status.........OK
```

## Notes

- If the execution "Status" field of the managed system shows SUCCESS, the console output of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
