# getraclog

## Description

The getraclog command displays RAC log entries.

## Synopsis

```bash
racadm getraclog [-i]
racadm getraclog [-s <start>] [-c <count>]
racadm getraclog [-c <count>] [-s <start-record>]
```

NOTE: If options are not provided, the entire log is displayed.

## Input

- `-c` — Specifies the number of records to display.
  - NOTE: On Local RACADM, the number of logs are restricted to 100 by default.
- `-s` — Specifies the starting record used for the display.
  - NOTE: When Enhanced Chassis Logging and Events feature is enabled, then -i and --more options are not displayed.

## Output

```
SeqNumber = 286
Message ID = USR0005
Category = Audit
AgentID = RACLOG
Severity = Information
Timestamp = 2017-05-15 06:25:27
Message = Login failed from processdisco06a: 192.168.0
Message Arg 1 = processdisco06a
Message Arg 2 = 10.92.68.245
FQDD = iDRAC.Embedded.1
```

## Example

Display the recent 2 records for RAC log

```bash
racadm getraclog -c 2
```

Output:

```
SeqNumber = 4102
Message ID = LIC201
Category = Audit
AgentID = DE
Severity = Warning
Timestamp = 2017-05-15 06:30:20
Message = License yPMRJGuEf7z5HG8LO7gh assigned to device iDRAC expires in 4 days.
Message Arg 1 = yPMRJGuEf7z5HG8LO7gh
Message Arg 2 = iDRAC
Message Arg 3 = 4
-------------------------------------------------------------------------
SeqNumber = 4101
Message ID = USR0032
Category = Audit
AgentID = RACLOG
Severity = Information
Timestamp = 2017-05-15 06:25:27
Message = The session for root from 192.168.0 using RACADM is logged off.
Message Arg 1 = root
Message Arg 2 = 10.94.98.92
Message Arg 3 = RACADM
FQDD = iDRAC.Embedded.1
-------------------------------------------------------------------------
```