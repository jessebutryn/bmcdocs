# NmCupsManage

Manages Compute Usage Per Second (CUPS) by Intel Intelligent Power Node Manager for Supermicro Intel platforms.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c NmCupsManage --type <type> --action <action> [options...]
```

### In-Band
```
saa -c NmCupsManage --type <type> --action <action> [options...]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c NmCupsManage --type <type> --action <action> [options...]
```

## Actions

Supported for `--type NM30` (Node Manager 3.0):

- **GetCUPSCapability**: Gets CUPS capability.
- **GetCUPSData**: Gets CUPS data.
- **GetCUPSConfig**: Gets CUPS configuration.
- **GetCUPSPolicy**: Gets CUPS policies.
- **GetCUPSCore**: Gets core CUPS utilization.
- **GetCUPSIO**: Gets IO CUPS utilization.
- **GetCUPSMem**: Gets memory CUPS utilization.
- **SetCUPSPolicy**: Sets CUPS policy.
- **EnableCUPSPolicy**: Enables CUPS policy.
- **DisableCUPSPolicy**: Disables CUPS policy.

## Options

- `--type <type>`: Manages CUPS with type. Supported: NM30.
- `--action <action>`: Manages CUPS with the action to perform (see Actions above).
- `--domain_id <Domain ID>`: Assigns domain ID. Used with SetCUPSPolicy, EnableCUPSPolicy, DisableCUPSPolicy: 1=Core Domain, 2=Memory Domain, 4=IO Domain.
- `--storage <Storage>`: Assigns storage (used with SetCUPSPolicy). 0=Persistent storage, 1=Volatile memory.
- `--alert <Alert>`: Assigns alert status (used with SetCUPSPolicy). 0=Disable alerting, 1=Enable sending of alert.
- `--threshold <Threshold>`: Assigns CUPS threshold (0-100) (used with SetCUPSPolicy).
- `--avg_windows <averaging window>`: Assigns averaging window in seconds (0-65535) (used with SetCUPSPolicy).

## Examples

### GetCUPSCapability
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCupsManage --type NM30 --action GetCUPSCapability
```

### GetCUPSData / GetCUPSConfig / GetCUPSPolicy
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCupsManage --type NM30 --action GetCUPSData
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCupsManage --type NM30 --action GetCUPSConfig
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCupsManage --type NM30 --action GetCUPSPolicy
```

### GetCUPSCore / GetCUPSIO / GetCUPSMem
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCupsManage --type NM30 --action GetCUPSCore
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCupsManage --type NM30 --action GetCUPSIO
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCupsManage --type NM30 --action GetCUPSMem
```

### SetCUPSPolicy
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCupsManage --type NM30 --action SetCUPSPolicy --domain_id 1 --storage 1 --alert 1 --threshold 50 --avg_window 2000
```

### EnableCUPSPolicy / DisableCUPSPolicy
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCupsManage --type NM30 --action EnableCUPSPolicy --domain_id 1
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c NmCupsManage --type NM30 --action DisableCUPSPolicy --domain_id 1
```

### In-Band
```bash
[SAA_HOME]# ./saa -c NmCupsManage --type NM30 --action GetCUPSCapability
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c NmCupsManage --type NM30 --action GetCUPSCapability
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

### GetCUPSCapability
```
CUPS Capabilities: CUPS feature is enabled
CUPS Policy : CUPS policies configuration available
CUPS version : 1
```

### GetCUPSData
```
CUPS Index: 0
CUPS Dynamic Load Factors:
 CPU CUPS dynamic Load factor : 0
 Memory CUPS dynamic Load factor : 0
 IO CUPS dynamic Load factor : 0
Base Utilization:
 Base CPU CUPS utilization value : 00 00 FF FF FF FF FF FF
Aggregate utilization values:
 Aggregate CPU CUPS utilization value : 4D 8C 9C 05 00 00 00 00
 Aggregate Memory CUPS utilization value : 0F 76 02 00 00 00 00 00
 Aggregate IO CUPS utilization value : 50 48 00 00 00 00 00 00
Utilization Average:
 Utilization average for the core domain : 0% (00 00 00 00 00 00 00 00)
 Utilization average for the memory domain : 0% (00 00 00 00 00 00 00 00)
 Utilization average for the IO domain : 0% (00 00 00 00 00 00 00 00)
```

### GetCUPSConfig
```
CUPS Feature Enabled Status : CUPS feature is enabled
Load Factor Configuration : Dynamic
Static Core Load Factor : 1
Static Memory Load Factor : 1
Static IO Load Factor : 1
```

### GetCUPSPolicy
```
CUPS Policy ID : Core Domain
Target identifier : BMC
Policy Status : Policy Enabled
Policy Storage : Persistent storage
Policy Excursion Actions : Sending of alert enabled
CUPS Threshold : 0
Averaging Window in sec : 6
CUPS Policy ID : Memory Domain
Target identifier : BMC
Policy Status : Policy Enabled
Policy Storage : Persistent storage
Policy Excursion Actions : Sending of alert enabled
CUPS Threshold : 0
Averaging Window in sec : 6
CUPS Policy ID : IO Domain
Target identifier : BMC
Policy Status : Policy Enabled
Policy Storage : Persistent storage
Policy Excursion Actions : Sending of alert enabled
CUPS Threshold : 0
Averaging Window in sec : 6
CUPS Policy ID : Core Domain
Target identifier : Remote Console
Policy Status : Policy Enabled
Policy Storage : Persistent storage
Policy Excursion Actions : Sending of alert enabled
CUPS Threshold : 0
Averaging Window in sec : 6
CUPS Policy ID : Memory Domain
Target identifier : Remote Console
Policy Status : Policy Enabled
Policy Storage : Persistent storage
Policy Excursion Actions : Sending of alert enabled
CUPS Threshold : 0
Averaging Window in sec : 6
CUPS Policy ID : IO Domain
Target identifier : Remote Console
Policy Status : Policy Enabled
Policy Storage : Persistent storage
Policy Excursion Actions : Sending of alert enabled
CUPS Threshold : 0
Averaging Window in sec : 6
```

### GetCUPSCore / GetCUPSIO / GetCUPSMem
```
Core CUPS = 0
```
```
IO CUPS = 0
```
```
Memory CUPS = 0
```

### SetCUPSPolicy
```
Done.
CUPS Policy ID : Core Domain
Target identifier : Remote Console
Policy Status : Policy Enabled
Policy Storage : Volatile memory
Policy Excursion Actions : Sending of alert enabled
CUPS Threshold : 50
Averaging Window in sec : 2000
```

### EnableCUPSPolicy / DisableCUPSPolicy
```
Done.
```

## Notes

- Starting from X14 and later platforms, the `--type NM30` option is not supported. These platforms do not have a Management Engine (ME) to support Intel Node Manager management.
- If the execution "Status" field for a managed system is SUCCESS, the console output of the managed system will be shown in the Execution Message section of the created log file.
