# infinibandstatistics

## Description

Displays the list of InfiniBand devices managed by the server for which statistics are available.

## Synopsis

```
racadm infinibandstatistics <Infiniband FQDD>
```

## Input

- `<Infiniband FQDD>` — The fully qualified device descriptor of the device.

## Output/Example

Display the statistics of all InfiniBand devices managed by the server.

```
racadm infinibandstatistics
```

Display the statistics of the InfiniBand specified by InfiniBand.Slot.3-1.

```
racadm infinibandstatistics InfiniBand.Slot.3-1
Device Description:
InfiniBand in Slot 3 Port 1 Partition 1
Port Transmit Data: 0
Port Receive Data: 0
Port Transmit Packets: 0
Port Receive Packets: 0
Port Transmit Wait: 0
```