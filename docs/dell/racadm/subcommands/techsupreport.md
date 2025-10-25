# techsupreport

## Description

Allows you to perform the technical support report operations.

Tech Support Report (TSR) is now known as SupportAssist Collections and the new term is used in all documentation and GUI. To maintain compatibility across server generations, the RACADM command has been retained as techsupreport.

The types of operations are:

- collect — Collects the technical support report data to export. You can specify the various types of logs to be in the report.
- export — Exports the collected Tech Support Report data. To run this subcommand, you must have the Execute Server Control Commands permission.
- getupdatetime — Gets the timestamp of the last operating system application data collection.
- updateosapp — Updates the operating system application data collection. To run this subcommand, you must have the Execute Server Control Commands permission.

## Synopsis

```
racadm techsupreport <tech support report command type>
racadm techsupreport collect [-t <type of logs>]
racadm techsupreport export -l <CIFS,NFS,TFTP,FTP> -u <username> -p <password>
racadm techsupreport getupdatetime
racadm techsupreport updateosapp -t <type of OS App logs>
racadm techsupreport export -f <filename>
```

## Input

- `-t` — Type of logs. You can specify any of the following values that are separated by a ',' (comma):
  - SysInfo — System Information
  - OSAppNoPII — Filtered OS and Application data
  - OSAppAll — OS and Application data
  - TTYLog — TTYLog data
- `-l` — Network share location to export the report
- `-u` — User name for the remote share to export the report
- `-p` — Password for the remote share to export the report
- `-f` — Target filename for the exported log (must have .zip extension)

## Output/Example

Collect the system information data.

```
racadm techsupreport collect —t <type of logs>
```

Collect the system information and TTYLog data.

```
racadm techsupreport collect -t SysInfo,TTYLog
```

Collect the operating system application data.

```
racadm techsupreport collect -t OSAppAll
```

Export the collected Tech Support Report, to an FTP share.

```
racadm techsupreport export -l ftp://192.168.0/share -u myuser -p xxx
```

Export the collected Tech Support Report, to a TFTP share.

```
racadm techsupreport export -l tftp://192.168.0/share
```

Export the collected Tech Support Report, to a CIFS share.

```
racadm techsupreport export -l //192.168.0/share -u myuser -p xxx
```

Export the collected Tech Support Report, to an NFS share.

```
racadm techsupreport export -l 192.168.0:/share
```

Export the collected Tech Support Report to the local file system.

```
racadm techsupreport export -f tsr_report.zip
```