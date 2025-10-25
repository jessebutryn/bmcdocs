# nicstatistics

## Description

Displays the statistics for the NIC FQDD.

## Synopsis

```
racadm nicstatistics
racadm nicstatistics <NIC FQDD>
```

## Input

- `<NIC FQDD>` — The fully qualified device descriptor of the NIC.

## Output/Example

Display the statistics for the integrated NIC.

```
racadm nicstatistics NIC.Integrated.1-1-1
Device Description: Integrated NIC 1 Port 1 Partition 1
Total Bytes Received: 0
Total Bytes Transmitted: 0
Total Unicast Bytes Received: 0
Total Multicast Bytes Received: 0
Total Broadcast Bytes Received: 0
Total Unicast Bytes Transmitted: 0
Total Multicast Bytes Transmitted: 0
Total Broadcast Bytes Transmitted: 0
FCS error packets Received: 0
Alignment error packets Received: 0
False Carrier error packets Received: 0
Runt frames Received: 0
Jabber error frames Received: 0
Total Pause XON frames Received: 0
Total Pause XOFF frames Received: 0
Discarded packets: 0
Single Collision frames Transmitted: 0
Multiple Collision frames Transmitted: 0
Late Collision frames Transmitted: 0
Excessive Collision frames Transmitted: 0
Link Status: Down
```