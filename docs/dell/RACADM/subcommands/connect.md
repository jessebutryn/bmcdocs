# connect

## Description

Allows you to connect to the switch or blade serial console.

**Note:** This subcommand is only supported on the firmware interface.

## Synopsis

```bash
racadm connect [-b] -m <module>
```

## Input

- `-b` — Binary mode. (If used, CMC must be reset to terminate connect.)
- `-m` — Module, can be:
  - `server-<n>` — where n = 1 to 16
  - `server-<nx>` — where n = 1 to 8 and x = a to d
  - `switch-n` — where n = 1 to 6 or <a1 | a2 | b1 | b2 | c1 | c2>

## Examples

- Connect to I/O Module 1: `racadm connect -m switch-1`
- Connect to server 1: `racadm connect -m server-1`