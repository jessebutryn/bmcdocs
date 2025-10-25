# ifconfig

## Description

Displays the contents of the network interface table.

To use this subcommand, you must have the Execute Diagnostic Commands permission.

## Synopsis

```
racadm ifconfig
```

## Input

N/A

## Output/Example

Display the network interface information.

```
racadm ifconfig
eth0      Link encap:Ethernet  HWaddr 00:1D:09:FF:DA:23
          inet addr:192.168.0.0  Bcast:192.168.0.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:2550665 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:272532097 (259.9 MiB)  TX bytes:0 (0.0 B)
```