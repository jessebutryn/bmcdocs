# ping

## Description

Verifies if the destination IP address is reachable from iDRAC with the current routing-table contents. A destination IP address is required. Based on the current routing-table contents, an ICMP echo packet is sent to the destination IP address.

To run this subcommand, you must have the Debug privilege.

## Synopsis

```bash
racadm ping <ipaddress>
```

## Input

- `<ipaddress>` — The IP address of the remote endpoint to ping.

## Output

```
PING 192.168.0 (192.168.0): 56 data bytes
64 bytes from 192.168.0: seq=0 ttl=64 time=4.121 ms
192.168.0 ping statistics
1 packets transmitted, 1 packets received, 0 percent packet loss
round-trip min/avg/max = 4.121/4.121/4.121 ms
```