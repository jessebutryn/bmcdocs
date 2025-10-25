# rollback

## Description

Allows you to roll back the firmware to an earlier version.

## Synopsis

```bash
racadm rollback <FQDD> [--reboot]
```

NOTE: To get the list of available rollback versions and FQDDs, run the racadm swinventory command.

## Input

- `<FQDD>`: Specify the FQDD of the device for which the rollback is required.
- `--reboot`: Performs a graceful system reboot after the BIOS firmware rollback.

## Examples

- To perform BIOS firmware rollback:
  ```bash
  racadm rollback iDRAC.Embedded.1-1
  ```
  Output:
  ```
  RAC1056: Rollback operation initiated successfully.
  ```

- To perform a graceful system reboot after BIOS firmware rollback:
  ```bash
  racadm rollback BIOS.Setup.1-1 --reboot
  ```