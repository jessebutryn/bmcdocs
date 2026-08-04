# GetEventLog

Shows the current system event log (including both BIOS and BMC event logs) from the managed system. With the `--file` option, the event log can be saved in an EventLog.txt file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetEventLog [--info | --mfg] | [--raw_data] [--no_banner] [--year | --month | --day] [--format CSV] [--redfish] [--file <EventLog.txt> [--overwrite]]
```

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c GetEventLog [--info | --mfg] | [--raw_data] [--no_banner] [--year | --month | --day] [--format CSV] [--file <EventLog.txt> [--overwrite]]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetEventLog [--info | --mfg] | [--raw_data] [--no_banner] [--year | --month | --day] [--format CSV] [--redfish] [--file <EventLog.txt> [--overwrite]]
```

## Options

- `--file <file name>`: Saves the event log to a file (prints on screen if the file-saving function is not available)
- `--overwrite`: Overwrites the output file
- `--raw_data`: Prints the raw data of each event log
- `--info`: Prints the current and total capacity of the event log
- `--mfg`: Prints general information of event logs in a style that complies with the manufacturer's assembly line requirements
- `--year <year>`: Filters event logs within n years
- `--month <month>`: Filters event logs within n months
- `--day <day>`: Filters event logs within n days
- `--format <file format>`: Saves the event log to a file in CSV format
- `--redfish`: Enables support for pure Redfish

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetEventLog
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetEventLog --raw_data
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetEventLog --info
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetEventLog --format csv --file EventLog
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetEventLog --month 1
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetEventLog --mfg
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetEventLog --redfish
```

### In-Band
```bash
[SAA_HOME]# ./saa -c GetEventLog --file EventLog.txt --no_banner --overwrite
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c GetEventLog --raw_data --file EventLog.txt
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetEventLog --file EventLog.txt
```

## Output

### Default
```
Event:1 Time:11/20/2022 16:58:35 Type:System
 Assertion: #0FF (System)| Event = Dedicated LAN Link Up
Event:2 Time:11/20/2022 16:58:45 Type:Power Supply
 Assertion: PS1 Status| Event = Presence detected
Event:3 Time:11/20/2022 16:58:46 Type:Voltage
 Assertion: CPU_VCCIN| Event = Lower Critical - going low
 Reading = 0.89 V, Threshold = 1.20 V
Event:4 Time:11/20/2022 16:58:46 Type:Voltage
 Assertion: CPU_VCCIN| Event = Lower Non-recoverable - going low
 Reading = 0.89 V, Threshold = 1.20 V
Event:5 Time:11/20/2022 17:01:33 Type:OS Boot
 Assertion: #000 (OS Boot)| Event = C: Boot completed
```

### --raw_data
```
SEL( 1) 01 00 02 BB 5C 7A 63 20 00 04 D0 FF 6F A3 01 FF
SEL( 2) 02 00 02 C5 5C 7A 63 20 00 04 08 C8 6F F0 FF FF
SEL( 3) 03 00 02 C6 5C 7A 63 20 00 04 02 13 01 52 34 47
SEL( 4) 04 00 02 C6 5C 7A 63 20 00 04 02 13 01 54 34 47
SEL( 5) 05 00 02 6D 5D 7A 63 41 00 04 1F 00 6F 01 FF FF
```

### --info
```
Total Entries: 32
SEL Version: 1.5
Free Space: 65535 bytes
Recent Entry Added: 2023/08/23 00:56:11
Recent Entry Erased: 2023/08/19 18:41:24
Number of alloc units: 512
Alloc unit size: 20 bytes
Number of free alloc unit: 480
Largest free blk: 480
```

### --mfg
```
Max record size: 20
Get/Set SEL Time: 2023/08/28 05:37:12
Event ID,Created Time,Sensor Type,Severity,Message,
1,2023-11-04T20:27:08Z,OEM,OK,[LAN-0005] Dedicated LAN Link Up,
2,2023-11-04T20:32:51Z,OEM,OK,[LAN-0003] System NIC (1) Link Up,
3,2023-11-04T20:32:51Z,OEM,Warning,[LAN-0004] System NIC (2) Link Down,
4,2023-11-04T20:37:54Z,OEM,OK,[LAN-0003] System NIC (1) Link Up,
5,2023-11-04T20:59:12Z,OEM,OK,[LAN-0003] System NIC (1) Link Up,
Event:1 Time:10/25/2023 09:02:05 Type:System
 Assertion: #0FF (System)| Event = Dedicated LAN Link Up
Event:2 Time:10/25/2023 09:02:16 Type:Physical Security (Chassis Intrusion)
 Assertion: Chassis Intru| Event = undefined
Event:3 Time:10/25/2023 09:02:22 Type:Temperature
 Assertion: M2_SSD2 Temp| Event = Upper Critical - going high
 Reading = 71.00 C, Threshold = 70.00 C
Event:4 Time:10/25/2023 09:08:00 Type:System
 Assertion: #0FF (System)| Event = Dedicated LAN Link Up
Event:5 Time:10/25/2023 09:08:10 Type:Physical Security (Chassis Intrusion)
 Assertion: Chassis Intru| Event = undefined
 1| 01/31/2023 01:15:55 | Assertion: PS1 Status | Type: Power Supply
 | Event = Presence detected
```

### --redfish
```
 2| 02/04/2023 15:56:06 | Assertion: VDimmABCD | Type: Voltage
 | Event = Upper Critical - going high
 | Reading = 2.04 V, Threshold = 1.37 V
 3| 02/04/2023 15:56:06 | Assertion: VDimmABCD | Type: Voltage
 | Event = Upper Non-recoverable - going high
 | Reading = 2.04 V, Threshold = 1.40 V
 4| 02/04/2023 15:56:15 | Deassertion: VDimmABCD | Type: Voltage
 | Event = Upper Non-recoverable - going high
 | Reading = 1.23 V, Threshold = 1.40 V
 5| 02/04/2023 15:56:15 | Deassertion: VDimmABCD | Type: Voltage
 | Event = Upper Critical - going high
 | Reading = 1.23 V, Threshold = 1.37 V
Event ID Created Time Sensor Type Severity Message
-------- ------------ ----------- -------- -------
 1 | 2024-03-30T19:14:05Z | OEM | OK | [LAN-0005] Dedicated LAN Link Up - Assert
 2 | 2024-03-30T19:16:39Z | OEM | OK | [LAN-0003] System NIC (1) Link Up - Assert
 3 | 2024-03-30T19:34:57Z | OEM | OK | [LAN-0003] System NIC (1) Link Up - Assert
 4 | 2024-03-30T19:34:57Z | OEM | Warning | [LAN-0004] System NIC (2) Link Down - Assert
 5 | 2024-03-30T19:40:44Z | OEM | OK | [LAN-0005] Dedicated LAN Link Up - Assert
```

## Notes

- If the execution "Status" field of the managed system shows SUCCESS, the console output of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
