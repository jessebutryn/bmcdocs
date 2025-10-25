# ping6

## Description

Verifies if the destination IPv6 address is reachable from iDRAC or with the current routing-table contents. A destination IPv6 address is required. Based on the current routing-table contents, an ICMP echo packet is sent to the destination IPv6 address.

To run this subcommand, you must have Debug privilege.

## Synopsis

```bash
racadm ping6 <ipv6address>
```

## Input

- `<ipv6address>` — the IPv6 address of the remote endpoint to ping.

## Example

```
Pinging 2011:de11:bdc:194::31 from 2011:de11:bdc:194::101 with 32 bytes of data:
Reply from 2011:de11:bdc:194::31: time<1ms
Reply from 2011:de11:bdc:194::31: time<1ms
Reply from 2011:de11:bdc:194::31: time<1ms
Reply from 2011:de11:bdc:194::31: time<1ms
Ping statistics for 2011:de11:bdc:194::31:
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
Minimum = 0ms, Maximum = 0ms, Average = 0ms
```