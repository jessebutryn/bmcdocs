# sensorsettings

## Description

Allows you to perform threshold settings of the sensor.

To run this subcommand, you must have Configure iDRAC privilege.

NOTE: An error message is displayed when the following is performed:

- A set operation is performed on an unsupported FQDD.
- Out of range settings is entered.
- Invalid sensor FQDD is entered.
- Invalid threshold level filter is entered.

## Synopsis

```bash
racadm sensorsettings set <FQDD> -level Min <value>
```

## Input

- `<FQDD>` — Sensor or corresponding sensor FQDD which needs a threshold configuration. Run the command, `racadm getsensorinfo` to view the sensor FQDD. The R/W field in the output getsensorinfo indicates if the sensor thresholds can be configured. Replace the <FQDD> field with the corresponding sensor FQDD that needs a threshold configuration.
- `-level` — threshold level for the sensor setting. Values are Max or Min.

## Examples

- To set the minimum noncritical threshold level for a power sensor type.
  ```bash
  racadm sensorsettings set iDRAC.Embedded.1#SystemBoardCPUUsage -level Max 95
  ```

NOTE: The entered value must be lesser or higher than the sensor critical threshold limit.