# GeneralNmManage

Manages a node manager by Intel Intelligent Power Node Manager (NM, `--type NM20`) or BMC Intel Node Manager (BMC-NM, `--type BMC10`) for Supermicro Intel platforms.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GeneralNmManage --type <type> --action <action> [options...]
```

### In-Band
```
saa -c GeneralNmManage --type <type> --action <action> [options...]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GeneralNmManage --type <type> --action <action> [options...]
```

## Actions

Supported for `--type NM20` (Intel Intelligent Power Node Manager):

- **GetNMSDR**: Displays NM sensor data record.
- **GetSelTime**: Gets system event log time.
- **GetStatistics**: Gets NM statistics.
- **ResetStatistics**: Resets NM statistics.
- **GetCapabilities**: Gets NM capabilities.
- **GetVersion**: Gets NM version.
- **GetAlert**: Gets NM alert.
- **SetAlert**: Sets NM alert.
- **GetTotalPower**: Gets total power budget.
- **SetTotalPower**: Sets total power budget.
- **DelTotalPower**: Deletes total power budget.
- **SetPowerDrawRange**: Sets NM power draw range.
- **GetSensor**: Gets sensor data.
- **GetSummary**: Gets NM summary information.

Supported for `--type BMC10` (BMC Intel Node Manager):

- **GetSelTime**: Gets system event log time.
- **GetStatistics**: Gets NM statistics.
- **ResetStatistics**: Resets NM statistics.
- **GetCapabilities**: Gets NM capabilities.
- **GetVersion**: Gets NM version.
- **GetTotalPower**: Gets total power budget.
- **SetTotalPower**: Sets total power budget.
- **DelTotalPower**: Deletes total power budget.
- **SetPowerDrawRange**: Sets NM power draw range.
- **GetSummary**: Gets NM summary information.

## Options

- `--type <type>`: Manages Intel Node Manager with type. Supported: NM20, BMC10.
- `--action <action>`: Manages Intel/BMC Node Manager with the action to perform (see Actions above).
- `--mode <type>`: Assigns mode (used with GetStatistics/ResetStatistics). For `--type NM20` GetStatistics: 1=Global power statistics [Watts], 2=Global inlet temperature [Celsius], 3=Global throttling statistics [%] (NM 3.0), 4=Global volumetric airflow statistics (NM 3.0), 5=Global outlet airflow temperature (NM 3.0), 6=Global chassis power statistics (NM 3.0), 17=Per policy power statistics, 18=Per policy trigger statistics, 19=Per policy throttling statistics (NM 3.0), 27=Global Host Unhandled Requests statistics, 28=Global Host Response Time statistics, 29=Global CPU throttling statistics, 30=Global memory throttling statistics, 31=Global Host Communication Failure statistics. For ResetStatistics: 1=Global power statistics, 2=Global inlet temperature statistics, 27-31 as above. For `--type BMC10` GetStatistics: 1=Global power, 2=Global inlet temperature, 3=Global throttling, 4=Global volumetric airflow, 5=Global outlet airflow temperature, 6=Global chassis power, 17=Per policy power, 18=Per policy trigger, 29=Global CPU throttling (deprecated), 30=Global memory throttling (deprecated). For BMC10 ResetStatistics: 0=global statistics (power and inlet temp), 1=per policy statistics, 27-31 as above.
- `--policy_id <Policy ID>`: Assigns policy ID. Applies for mode 11h/12h (NM20) or 11h/13h (BMC10) GetStatistics; otherwise set to 0. Ignored for ResetStatistics if mode is 0h (NM20) or 1h (BMC10).
- `--domain_id <Domain ID>`: Assigns domain ID. For `--type NM20`: 0=Entire platform, 1=CPU subsystem, 2=Memory subsystem, 3=HW Protection (NM 3.0), 4=High Power I/O subsystem. For `--type BMC10`: 0=Entire platform AC power (Psys support required), 1=CPU subsystem, 2=Memory subsystem, 4=PCIe devices subsystem (Psys support required), 5=Entire platform DC power (Psys support required). For mode in range 1Bh-1Fh, Domain ID must be set to 00h.
- `--trigger_type <Trigger Type>`: Assigns trigger type (used with GetCapabilities). For `--type NM20`: 0=No Policy Trigger, 1=Inlet Temperature Policy Trigger [Celsius], 2=Missing Power Reading Timeout [1/10th sec], 3=Time After Host Reset Trigger [1/10th sec], 4=Boot time policy, 6=MGPIO Policy Trigger. For `--type BMC10`: 0=No Policy Trigger, 1=Inlet Temperature Policy Trigger, 2=Missing Power Reading Timeout, 3=Time After Host Reset Trigger, 6=GPIO Policy Trigger, 7=C0 Residency [%], 8=Host Reset, 9=SMBAlert Interrupt.
- `--value <Assignment value>`: Assigns value. Used with SetAlert (SNMP sequence 1-15, check via SnmpManage command) and SetTotalPower (watts).
- `--range <Range>`: Assigns value range for SetPowerDrawRange. Power draw range: 0-32767.
- `--per_component_control <Per-component Control>`: Allows for setting/getting the power budget for a chosen domain component (`--type BMC10` GetTotalPower/SetTotalPower/DelTotalPower). 0=Applied to whole domain (persistent setting), 1=Applied to given component in domain (volatile setting).
- `--component_id <Component ID>`: Assigns a component ID. Applies when `--per_component_control` is set to 1. For the CPU Domain: CPU socket number (0-7). For the Memory Domain: CPU socket number (0-7) associated with memory channels. For the PCIe Domain: PCIe card index.

## Examples

### GetNMSDR (NM20)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GeneralNmManage --type NM20 --action GetNMSDR
```

### GetSelTime (NM20)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GeneralNmManage --type NM20 --action GetSelTime
```

### GetStatistics (NM20)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GeneralNmManage --type NM20 --action GetStatistics --mode 1 --domain_id 0 --policy_id 0
```

### ResetStatistics (NM20)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GeneralNmManage --type NM20 --action ResetStatistics --mode 0 --domain_id 0 --policy_id 0
```

### GetCapabilities (NM20)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GeneralNmManage --type NM20 --action GetCapabilities --domain_id 0 --trigger_type 0
```

### GetVersion (NM20)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GeneralNmManage --type NM20 --action GetVersion
```

### GetAlert / SetAlert (NM20)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GeneralNmManage --type NM20 --action GetAlert
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GeneralNmManage --type NM20 --action SetAlert --value 1
```

### GetTotalPower / SetTotalPower / DelTotalPower (NM20)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GeneralNmManage --type NM20 --action GetTotalPower --domain_id 0
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GeneralNmManage --type NM20 --action SetTotalPower --domain_id 0 --value 100
[SAA_HOME]# ./saa -c GeneralNmManage --type NM20 --action DelTotalPower --domain_id 0
```

### SetPowerDrawRange (NM20)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GeneralNmManage --type NM20 --action SetPowerDrawRange --domain_id 0 --range 0-32767
```

### GetSensor / GetSummary (NM20)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GeneralNmManage --type NM20 --action GetSensor
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GeneralNmManage --type NM20 --action GetSummary
```

### GetStatistics (BMC10, with per-component control)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GeneralNmManage --type BMC10 --action GetStatistics --mode 1 --domain_id 1 --policy_id 1 --per_component_control 0 --component_id 0
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GeneralNmManage --type BMC10 --action GetStatistics --mode 2 --domain_id 2 --policy_id 0 --per_component_control 1 --component_id 0
```

### GetTotalPower / SetTotalPower / DelTotalPower (BMC10)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GeneralNmManage --type BMC10 --action GetTotalPower --domain_id 0 --per_component_control 1 --component_id 0
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GeneralNmManage --type BMC10 --action SetTotalPower --domain_id 0 --value 100 --per_component_control 1 --component_id 0
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GeneralNmManage --type BMC10 --action DelTotalPower --domain_id 0 --per_component_control 1 --component_id 0
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GeneralNmManage --type NM20 --action GetSummary
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

## Output

### GetNMSDR
```
Record ID = 1C 00
SDR Version = 51h
Record Type = C0h
Record Length = 0Bh
OEM ID = 57 01 00 h
Record Subtype = 0Dh
SubType Version = 01h
Slave Address = 2Ch
Channel = 00h
Health Event Sensor Number = 1Dh
Exception Event Sensor Number = 1Eh
Operational Capabilities Sensor Number = 1Fh
Alert Threshold Exceeded Sensor Number = 20h
```

### GetSelTime
```
SEL Time = 2023/08/25 08:38:02
```

### GetVersion (NM20)
```
Node Manager Version = 2.0
```

### GetVersion (BMC10)
```
BMC Intel Node Manager = 1.0
```

### GetTotalPower (BMC10)
```
Total Power Budget in [Watts] = 100
```

### GetSensor
```
| Id | Sensor | Reading | Low Limit | High Limit |
| ------ | ---------------------------------------- | -------- | --------- | ---------- |
| 8 | PCH Thermal Threshold | 43C/109F | 2C/36F | 95C/203F |
| 32 | CPU 0 Thermal Control Circuit Activation | 0 % | 0 % | 0 % |
| 52 | CPU 0 Memory Throttling | 0 % | 0 % | 0 % |
| 163 | Inlet Airflow Temperature | 36C/97F | 0C/32F | 247C/477F |
| 173 | Total Chassis power | 4 W | 0 W | 0 W |
| 190 | Core CUPS | 0 % | N/A | N/A |
| 191 | IO CUPS | 0 % | N/A | N/A |
| 192 | Memory CUPS | 0 % | N/A | N/A |
| ------ | --------- | ---- | --------- | ---------- |
| 28 | CPU 0 Thermal Status | Normal |
| 36 | CPU 0 T-Control | 8 |
| 48 | CPU 0 T-JMAX | 93 |
```

### GetSummary (NM20)
```
Intel Intelligent Power Node Manager 6.0 (6.0.4.70)
SEL Time - 2023/08/25 09:57:53
Node Manager Policy: Not set
Total Power Budget: Not set
DCMI Power Limit: Disabled or not set
CUPS Policy: Not set
 CPU Information
+------------------------------------+
| P-State| T-State| Max Allowed Cores|
+====================================+
| 0/16| 0/1| 32/32|
+------------------------------------+
 Power Usage
+------------------------------------+
|Domain | Usage (W)|
+====================================+
|Entire platform | 114|
+------------------------------------+
|CPU subsystem | 0|
+------------------------------------+
|Memory subsystem | 4|
+------------------------------------+
 CUPS Utilization
+------------------------------------+
|Domain | Usage (%)|
+====================================+
|Core | 0|
+------------------------------------+
|Memory | 0|
+------------------------------------+
|IO | 0|
+------------------------------------+
```

### GetStatistics (BMC10)
```
Current = 66 w
Minimum = 0 w
Maximum = 72 w
Average = 67 w
Time = 2024/04/08 03:55:25
Reporting Period = 384609 sec
Domain ID:
 CPU subsystem
Policy/Global Administrative state:
 NM Policy Control is Globally Enabled
Measurements state:
 Measurements in progress
raw = 57 01 00 42 00 00 00 48 00 43 00 AD 6A 13 66 61 DE 05 00 51
```

## Notes

- Starting from X14 and later platforms, use `--type BMC10` instead of `NM20`. These platforms do not have a Management Engine (ME) to support Intel Node Manager management.
- When managing the Node Manager by BMC Intel Node Manager (`--type BMC10`), some domain management requires Platform Power (Psys) support. The `--domain_id` values 0 (Entire platform, AC power), 4 (PCIe devices subsystem), and 5 (Entire platform, DC power) require Psys support.
- If the execution "Status" field for a managed system is SUCCESS, the console output of the managed system will be shown in the Execution Message section of the created log file.
