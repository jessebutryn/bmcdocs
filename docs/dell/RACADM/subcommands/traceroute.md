# traceroute

## Description

Traces network path of the routers as the packets traverse from the system to a destination IPv4 address.

To run this subcommand, you must have the Execute Diagnostic Commands permission.

## Synopsis

```
racadm traceroute <IPv4 address>
```

## Input

- `<IPv4 address>` — Specifies IPv4 address.

## Output/Example

Trace the route to an IPv4 address.

```
racadm traceroute 192.168.0.1
traceroute to 192.168.0.1 (192.168.0.1), 30 hops max, 40 byte packets
1 192.168.0.1 (192.168.0.1) 0.801 ms 0.246 ms 0.253 ms
```