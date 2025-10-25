# traceroute6

## Description

Traces the network path of routers as the packets traverse from the system to a destination IPv6 address.

To run this subcommand, you must have the Execute Diagnostic Commands permission.

## Synopsis

```
racadm traceroute6 <IPv6address>
```

## Input

- `<IPv6address>` — Specifies IPv6 address.

## Output/Example

Trace the route to an IPv6 address.

```
racadm traceroute6 fd01::1
traceroute to fd01::1 (fd01::1) from fd01::3,
30 hops max, 16 byte packets
1 fd01::1 (fd01::1) 14.324 ms 0.26 ms 0.244 ms
```