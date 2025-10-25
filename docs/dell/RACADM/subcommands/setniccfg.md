# setniccfg

## Description

Sets the iDRAC IP address for static and DHCP modes.

To run this subcommand, you must have the Configure iDRAC privilege.

NOTE: The terms NIC and Ethernet management port may be used interchangeably.

## Synopsis

```
racadm setniccfg -d
racadm setniccfg -d6
racadm setniccfg -s <IPv4Address> <netmask> <IPv4 gateway>
racadm setniccfg -s6 <IPv6 Address> <IPv6 Prefix Length> <IPv6 Gateway>
racadm setniccfg -o
```

## Input

- `-d` — Enables DHCP for the NIC. It is enabled by default.
- `-d6` — Enables AutoConfig for the NIC (default is disabled).
- `-s` — Enables static IP settings. The IPv4 address, netmask, and gateway must be specified. Otherwise, the existing static settings are used. <ipaddress>, <netmask>, and <gateway> must be typed as dot-separated strings.

```
racadm setniccfg -s 192.168.0 255.255.255.0 192.168.0
```

- `-s6` — Enables static IPv6 settings. The IPv6 address, Prefix Length, and the IPv6 Gateway can be specified.
- `-o` — Enable or disable NIC.

## Output/Example

Configure static IPv4 address for iDRAC NIC

```
racadm setniccfg -s 192.168.0 255.255.255.0 192.168.0
```

```
Static IP configuration enabled and modified successfully
```

Configure DHCP mode for iDRAC IPv4

```
racadm setniccfg -d
```

```
DHCP is now ENABLED
```

Configure DHCP mode for iDRAC IPv6

```
racadm setniccfg -d6
```

```
DHCP6 is now ENABLED
```