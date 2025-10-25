# networktransceiverstatistics

## Description

Displays the statistics for the list of NIC transceivers.

NOTE: The target server must have iDRAC Datacenter license to run this command.

## Synopsis

```
racadm networktransceiverstatistics
racadm networktransceiverstatistics <PORT FQDD>
racadm networktransceiverstatistics -all
```

## Input

- `<PORT FQDD>` — Fully qualified device descriptor of the NIC
- `-all` — For all the available network transceivers

## Output/Example

Display the available network transceivers managed by the server for statistics.

```
racadm networktransceiverstatistics
```

Display the statistics of the network transceiver specified by NIC.Integrated.1-1-1.

```
racadm networktransceiverstatistics NIC.Integrated.1-1-1
```

Display the statistics of all the network transceivers managed by the server.

```
racadm networktransceiverstatistics -all
```