# clearpending

## Description

Deletes the pending values of all the attributes (objects) in the device (NIC, BIOS, FC, and Storage).

**Note:** If any attribute is not modified or a job is already scheduled for the same device, then the pending state is not cleared or deleted.

## Synopsis

```bash
racadm clearpending <FQDD>
```

## Input

- `<FQDD>` — The Fully Qualified Device Descriptor:
  - BIOS FQDD
  - NIC FQDD
  - Infiniband FQDD
  - FC FQDD
  - Storage controller FQDD

## Output

A message is displayed indicating that the pending state is cleared or deleted.

## Examples

- Clear NIC pending: `racadm clearpending NIC.Integrated.1-1`
- Clear InfiniBand pending: `racadm clearpending <InfiniBand FQDD>`