# getsensorinfo

## Description

Displays the status for system sensors.

NOTE: For the Dell PowerEdge FX2 chassis with the FM120x4 server, the power-related information is not displayed.

## Synopsis

```bash
racadm getsensorinfo
racadm getsensorinfo -c
```

## Input

- `-c` — Compact output format.

NOTE: Chassis Controller is supported only on PowerEdge FX2, and GPU sensors are displayed only on PowerEdge C4140 servers.

## Example

```bash
racadm getsensorinfo
```

Displays the status for all system sensors.