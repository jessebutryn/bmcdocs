# gettracelog

## Description

Lists all the trace login entries of iDRAC.

## Synopsis

```
racadm gettracelog [-i]
racadm gettracelog [-s <start>] [-c <count>]
```

## Input

- `-i` — Displays the number of entries in iDRAC trace log.
- `-c` — Specifies the number of records to display.
- `-s` — Specifies the starting record to display.

## Output/Example

The default output display shows the record number, timestamp, source and description. The timestamp begins at midnight, January 1 and increases until the system starts. After the system starts, the system's timestamp is used.

Display entire log

```
racadm gettracelog
```

Display number of records in log

```
racadm gettracelog -i
```

```
Total Records: 228
```