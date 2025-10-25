# recover

## Description

Allows you to recover the previous version of the firmware.

NOTE: To run this subcommand, you must have the Server Control privilege.

## Synopsis

- To recover the BIOS firmware:

```
racadm recover <FQDD>
```

NOTE: BIOS.Setup.1-1 is the supported FQDD

## Input

- `<FQDD>` — Specify the FQDD of the device for which the recovery is required.

## Output/Example

To recover the BIOS firmware:

```
racadm recover BIOS.Setup.1-1
```

```
RAC1234: Recovery operation initiated successfully. Check the Lifecycle logs for the status of the operation by running RACADM command "racadm lclog view".
```