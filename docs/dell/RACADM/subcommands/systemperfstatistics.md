# systemperfstatistics

## Description

Allows you to view and manage the system performance monitoring operations.

## Synopsis

```bash
racadm systemperfstatistics view
racadm systemperfstatistics <sensor_FQDD>
racadm systemperfstatistics PeakReset <FQDD>
```

## Examples

- To view the FQDD's of system performance monitoring sensors
  ```bash
  racadm systemperfstatistics view
  ```
  Output:
  ```
  [key = iDRAC.Embedded.1#SystemBoardCPUUsageStat]
  [key = iDRAC.Embedded.1#SystemBoardIOUsageStat]
  [key = iDRAC.Embedded.1#SystemBoardMEMUsageStat]
  [key = iDRAC.Embedded.1#SystemBoardSYSUsageStat]
  ```

- To list the usage statistics of a specific sensor
  ```bash
  racadm systemperfstatistics iDRAC.Embedded.1#SystemBoardCPUUsageStat
  ```
  Output:
  ```
  Minimum Readings
  Last Hour = 0% [At Mon, 05 May 2017 17:13:04]
  Last Day = 0% [At Mon, 05 May 2017 15:59:53]
  Last Week = 0% [At Mon, 05 May 2017 15:59:53]
  Maximum Readings
  Last Hour = 0% [At Thu, 01 Jan 1970 00:00:00]
  Last Day = 0% [At Thu, 01 Jan 1970 00:00:00]
  Last Week = 0% [At Thu, 01 Jan 1970 00:00:00]
  Average Readings
  Last Hour = 0%
  Last Day = 0%
  Last Week = 0%
  ```