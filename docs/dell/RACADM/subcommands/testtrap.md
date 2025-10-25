# testtrap

## Description

Tests the RAC's SNMP trap alerting feature by sending a test trap from iDRAC to a specified destination trap listener on the network.

To run this subcommand, you must have the Test Alert permission.

NOTE: Before you run the testtrap subcommand, make sure that the specified index in the RACADM iDRAC.SNMPAlert group is configured properly. The indices of testtrap subcommand is co-related to the indices of iDRAC.SNMPAlert group.

## Synopsis

```
racadm testtrap -i <index>
```

## Input

- `-i <index>` — Specifies the index of the trap configuration that must be used for the test. Valid values are from 1 to 4.

## Output/Example

Enable the alert.

```
racadm set idrac.emailalert.1.CustomMsg 1
racadm set iDRAC.SNMPAlert.1.Enable 1
```

Set the destination email IP address.

```
racadm set iDRAC.SNMPAlert.1.Destination 192.168.0
```

View the current test trap settings.

```
racadm get iDRAC.SNMPAlert.<index>
```

Test a trap with index as 1.

```
racadm testtrap -i 1
Test trap sent successfully.
```