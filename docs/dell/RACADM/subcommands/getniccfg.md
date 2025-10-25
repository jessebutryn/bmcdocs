# getniccfg

## Description

Displays the current and static NIC settings for iDRAC.

## Synopsis

```
racadm getniccfg
```

## Output/Example

The getniccfg subcommand displays an appropriate error message if the operation is not successful. Otherwise, the output is displayed in the following format:

IPv4 settings:

```
NIC Enabled=1
IPv4 Enabled=1
DHCP Enabled=0
IP Address=10.94.227.207
Subnet Mask=255.255.255.0
Gateway=10.94.227.1
```

IPv6 settings:

```
IPv6 Enabled=Disabled
DHCP6 Enabled=Enabled
IP Address 1=::
Gateway=::
Link Local Address=::
IP Address 2=::
IP Address 3=::
IP Address 4=::
IP Address 5=::
IP Address 6=::
IP Address 7=::
IP Address 8=::
IP Address 9=::
IP Address 10=::
IP Address 11=::
IP Address 12=::
IP Address 13=::
IP Address 14=::
IP Address 15=::
```

LOM Status:

```
NIC Selection=dedicated
Link Detected=Yes
Speed=1Gb/s
Duplex Mode=Full Duplex
```