# gethostnetworkinterfaces

## Description

Displays host network interface details.

NOTE: To run this subcommand, you must have iDRAC Service Module installed on the server operating system.

## Synopsis

```
racadm gethostnetworkinterfaces
racadm gethostnetworkinterfaces <NIC FQDD>
```

## Output/Example

To display the details of all the network interfaces on the server.

```
racadm gethostnetworkinterfaces
```

```
Local Area Connection 12
Description : iDRAC Virtual NIC USB Device #8
Status : Up
Interface Type : Ethernet
DHCP : Enabled
DHCPServerV4 : 169.254.0.1
MAC Address : 00-25-64-F9-7A-E7
IPv4 Address : 169.254.0.2
Subnet Mask : 255.255.255.0
IPv6 Address : fe80::1cce:a0a7:f30e:54fc
Prefix Length : 64
IPv6 DNSServer Address 0: fec0:0:0:ffff::1
IPv6 DNSServer Address 1: fec0:0:0:ffff::2
IPv6 DNSServer Address 2: fec0:0:0:ffff::3
```

To display the details of a particular NIC on the server.

```
racadm gethostnetworkinterfaces NIC.Integrated.1-1-1
```

```
Local Area Connection
Description : Broadcom NetXtreme Gigabit Ethernet
Status : Up
Interface Type : Ethernet
DHCP : Enabled
DHCPServerV4 : 10.94.224.25
MAC Address : 14-FE-B5-FF-B1-9C
FQDD : NIC.Integrated.1-1-1
IPv4 Address : 10.94.225.189
Subnet Mask : 255.255.255.128
IPv6 Address : fe80::7c5f:a114:84d4:17f6
Prefix Length : 64
IPv4 Gateway Address : 10.94.225.129
IPv4 DNSServer Address 0: 10.116.2.250
IPv4 DNSServer Address 1: 10.116.2.251
```