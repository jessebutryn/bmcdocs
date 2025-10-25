# GetEventLog

## Description

Use the "GetEventLog" command to execute SUM to show the current system event log (including both BIOS and BMC event log) from the managed system. With the --file option, the event log can be saved in the EventLog.txt file.

## Syntax

```
sum [[-i <IP or host name> | -I Redfish_HI] -u <username> -p <password>] -c GetEventLog [--file <EventLog.txt>] [--overwrite] [--raw_data] [--redfish] [--no_banner]
```

## Options

- `--file <EventLog.txt>`: Saves the event log to the specified file.
- `--overwrite`: Overwrites the output file if it exists.
- `--raw_data`: Displays the event log in raw data format.
- `--redfish`: Displays the event log in Redfish format.
- `--no_banner`: Suppresses the banner in the output.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetEventLog
The console output contains the following information.
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

```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetEventLog --raw_data
The console output contains the following information.
SEL( 1) 01 00 02 BB 5C 7A 63 20 00 04 D0 FF 6F A3 01 FF
SEL( 2) 02 00 02 C5 5C 7A 63 20 00 04 08 C8 6F F0 FF FF
SEL( 3) 03 00 02 C6 5C 7A 63 20 00 04 02 13 01 52 34 47
SEL( 4) 04 00 02 C6 5C 7A 63 20 00 04 02 13 01 54 34 47
SEL( 5) 05 00 02 6D 5D 7A 63 41 00 04 1F 00 6F 01 FF FF
```

```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetEventLog --redfish
The console output contains the following information.
Event ID Created Time Sensor Type Severity Message
-------- ------------ ----------- -------- -------
1 | 2024-01-09T18:29:09Z | System NIC | OK | [LAN-0005] Dedicated LAN Link Up
2 | 2024-01-09T18:32:01Z | System NIC | OK | [LAN-0003] System NIC (1) Link Up
3 | 2024-01-09T18:33:47Z | Power Supply | OK | [PWR-0000] PS2 Status, Power
Supply Installed
```

### In-Band
```
[SUM_HOME]# ./sum -c GetEventLog --file EventLog.txt --no_banner --overwrite
```

```
[SUM HOME]# ./sum -I Redfish_HI -u ADMIN -p PASSWORD -c GetEventLog --raw_data --file EventLog.tx
```
