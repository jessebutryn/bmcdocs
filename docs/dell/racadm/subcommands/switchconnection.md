# switchconnection

## Description

Provides the switch port details of iDRAC and server network ports. Refresh switch port details of all ports in the server.

To run this command, you must have the Login privilege.

## Synopsis

```
racadm switchconnection view
racadm switchconnection view [iDRAC FQDD | NIC FQDD]
racadm switchconnection refresh
```

## Input

- `<iDRAC FQDD | NIC FQDD>` — Is the fully qualified device descriptor of iDRAC or NIC.

## Output/Example

Provide switch port details of all iDRAC and server network port.

```
racadm switchconnection view
```

Provide switch port details of requested FQDD NIC.Integrated.1-1-1:BRCM.

```
racadm switchconnection view NIC.Integrated.1-1-1:BRCM
```

Refresh switch port details of all ports in the server.

```
racadm switchconnection refresh
```