# getsel

## Description

Displays all system event log (SEL) entries in iDRAC.

## Synopsis

```bash
racadm getsel [-i]
racadm getsel [-s <start>][-c <count>]
```

NOTE: If no arguments are specified, the entire log is displayed.

## Input

- `-i` — Displays the number of entries in the SEL.
- `-s` — Displays the starting record number.
- `-c` — Specifies the number of records to display.
- `--more` — Displays a screen.
  - NOTE: Press Q to exit from the screen.
- `-A` — Does not display headers or labels.
- `-o` — Displays each record on a single line.
- `-E` — Displays RAW SEL data along with the other data.
- `-R` — Displays only the RAW SEL data for each record

## Example

- Display entire log.
  ```bash
  racadm getsel
  ```

- Display number of records in log.
  ```bash
  racadm getsel -i
  ```