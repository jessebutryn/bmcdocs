# getsysinfo

## Description

Displays information related to iDRAC, managed system, and watchdog configuration.

NOTE: The hostname and OS Name fields in the getsysinfo output display accurate information only if the OpenManage Server Administrator (OMSA) is installed on the managed system. If OMSA is not installed these fields may be blank or inaccurate. An exception to this are the VMware and Windows operating system names, which are displayed even if OMSA is not installed on the managed system.

## Synopsis

```
racadm getsysinfo [-d] [-A] [-c] [-4] [-6]
```

## Input

- `-4` — Displays IPv4 settings
- `-6` — Displays IPv6 settings
- `-c` — Displays common settings
- `-d` — Displays iDRAC information
- `-A` — Eliminates the printing of headers or labels

## Output/Example

RAC Information:

```
RAC Date/Time = Fri May 5 10:56:23 2017
Firmware Version = 3.00.00.00
Firmware Build = 62
Last Firmware Update = 05/02/2017 06:49:43
Hardware Version = 0.01
MAC Address = 84:7b:eb:d5:03:e0
SVC Tag = BDC14GH
```

Common settings:

```
Register DNS RAC Name = 1
DNS RAC Name = ipmierrata
Current DNS Domain = sha512.com
Domain Name from DHCP = Disabled
```

IPv4 settings:

```
Enabled = 1
Current IP Address = 10.94.195.33
Current IP Gateway = 10.94.195.1
Current IP Netmask = 255.255.255.0
DHCP Enabled = 1
Current DNS Server 1 = 10.94.192.67
Current DNS Server 2 = 0.0.0.0
DNS Servers from DHCP = Disabled
```

IPv6 settings:

```
Enabled = 1
Current IP Address 1 = 2011:de11:bdc:195::16e/64
Current IP Gateway = fe80::21c:23ff:fe6a:1106
Autoconfig = 1
Link Local IP Address = fe80::ba2a:72ff:fefc:4fb0/64
Current IP Address 2 = ::
Current IP Address 3 = ::
...
DNS Servers from DHCPv6 = Disabled
Current DNS Server 1 = 2011:de11:bdc:192::67/64
Current DNS Server 2 = ::
```

System Information:

```
System Model = PowerEdge R740
System Revision = I
System BIOS Version = 2.3.10
Service Tag = C9J69R2
Express Svc Code = 26697788894
Host Name = WIN-NIO9S113L98
OS Name = Windows Server 2019
OS Version = 10.0
Power Status = ON
Fresh Air Capable = No
RollupStatus = Ok
```

Display system information

```
racadm getsysinfo -c
```

Display iDRAC information

```
racadm getsysinfo -d
```

Display IPv4 details without header

```
racadm getsysinfo -A
```

```
"RAC IPv4 Information:"
```