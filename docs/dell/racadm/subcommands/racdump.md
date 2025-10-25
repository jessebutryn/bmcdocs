# racdump

## Description

Provides a single command to get dump, status, and general iDRAC board information.

To run this subcommand, you must have the Debug permission.

- General System/RAC Information
- Coredump Information
- Network Interface Statistics
- Session Information
- Process Information
- RAC Firmware Build Log

NOTE: The RAC debug logs are not part of Local and Remote RACADM. It is available only on Firmware RACADM

## Synopsis

```
racadm racdump
```

## Output/Example

===============================================================================
General System/RAC Information
=============================================================================== RAC
Information: RAC Date/Time = Thu May 18 13:35:32 2017 Firmware Version = 3.00.00.00
Firmware Build = 12 Last Firmware Update = 04/04/2017 19:41:38 Hardware Version = 0.01
MAC Address = 18:03:73:F7:B7:CA Common settings: Register DNS RAC Name = 0 DNS RAC Name
= idrac Current DNS Domain = Domain Name from DHCP = Disabled IPv4 settings: Enabled =
1 Current IP Address = 192.168.0.1 Current IP Gateway = 192.168.0.1 Current IP Netmask
= 192.168.0.1 DHCP Enabled = 0 Current DNS Server 1 = 0.0.0.0 Current DNS Server 2 =
0.0.0.0 DNS Servers from DHCP = Disabled IPv6 settings: Enabled = 0 Current IP Address
1 = :: Current IP Gateway = :: Autoconfig = 1 Link Local IP Address = :: Current
IP Address 2 = :: Current IP Address 3 = :: Current IP Address 4 = :: Current IP
Address 5 = :: Current IP Address 6 = :: Current IP Address 7 = :: Current IP Address
8 = :: Current IP Address 9 = :: Current IP Address 10 = :: Current IP Address 11
= :: Current IP Address 12 = :: Current IP Address 13 = :: Current IP Address 14 = ::
Current IP Address 15 = :: DNS Servers from DHCPv6 = Disabled Current DNS Server 1
= :: Current DNS Server 2 = :: System Information: System Model = PowerEdge R720 System
Revision = I System BIOS Version = 3.0.00 Service Tag = Express Svc Code = Host Name
= localhost.localdomain OS Name = OS Version = Power Status = ON Fresh Air Capable =
No Watchdog Information: Recovery Action = None Present countdown value = 478 seconds
Initial countdown value = 480 seconds Embedded NIC MAC Addresses: NIC.Integrated.1-3-1
Ethernet = 78:2B:CB:4B:C2:ED NIC.Integrated.1-1-1 Ethernet = 78:2B:CB:4B:C2:EB
=============================================================================== Coredump
Information ===============================================================================
There is no coredump currently
available. ===============================================================================
Network Interface Statistics
=============================================================================== Kernel IPv6
routing table Destination Next Hop Flags Metric Ref Use Iface ::1/128 :: U 0 1 1
lo ::1/128 :: U 256 0 0 lo fe80::1a03:73ff:fef7:b7ca/128 :: U 0 0 1 lo fe80::/64 ::
U 256 0 0 eth1 ff00::/8 :: U 256 0 0 eth1 Kernel IP routing table Destination Gateway
Genmask Flags MSS Window irtt Iface 0.0.0.0 192.168.0.1 0.0.0.0 UG 0 0 0 bond0 192.168.0.1
0.0.0.0 192.168.0.1 U 0 0 0 bond0 Active Internet connections (w/o servers) Proto Recv-
Q Send-Q Local Address Foreign Address State tcp 0 0 192.168.0.1:53986 192.168.0.1:199
ESTABLISHED tcp 0 0 192.168.0.1:53985 192.168.0.1:199 ESTABLISHED tcp 0 0 192.168.0.1:199
192.168.0.1:53986 ESTABLISHED tcp 0 0 192.168.0.1:199 192.168.0.1:53985 ESTABLISHED
=============================================================================== Session
Information ===============================================================================
No active sessions currently exist.
=============================================================================== Process
Information ===============================================================================
PID USER VSZ STAT COMMAND 1 root 5236 S {systemd} /sbin/init 2 root 0 SW [kthreadd]
3 root 0 SW [ksoftirqd/0] 6 root 0 SW [watchdog/0] 7 root 0 SW< [khelper] 8 root 0
SW [netns] 153 root 0 SW [sync_supers] 155 root 0 SW [bdi-
default] 157 root 0 SW< [kblockd] 166 root 0 SW [khubd] 16233 root 40916 S racadm racdump
16246 root 3824 S sh -c /bin/ps 16247 root 3828 R /bin/ps 26851 root 0 SW [kworker/
u:3] ===============================================================================
RAC Firmware Build Log
===============================================================================
BLD_TAG=idracfw_bldtag_3.00.00.00_691231_1800_00 BLD_VERSION=3.00.00.00 BLD_NUMBER=69.12.31
BLD_DATE=2.00.00.00.733 BLD_TYPE=idrac BLD_KERNEL=ZIMAGE