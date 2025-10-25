# getversion

## Description

Displays the current software version, model and generation information, and whether the target device can be updated.

## Synopsis

```
racadm getversion
racadm getversion [-b | -c | —i]
racadm getversion [-f <filter>]
```

## Input

- `-c` — Displays the server's current CPLD version.
- `-b` — Displays the server's current BIOS version.
- `-i` — Displays the server's current IDSDM version.
- `-f <filter>` — Filters the components and must be one of the following values:
  - `bios`: BIOS
  - `idrac`: iDRAC
  - `lc`: Lifecycle Controller
  - `idsdm`: SD card

## Output/Example

```
racadm getversion -c
```

```
< Server > < CPLD Version > < Blade Type >
server-1 1.0.5 PowerEdge M520
server-2 1.0.3 PowerEdge M610x
server-4 1.0.0 PowerEdge M710HD
server-5 1.0.3 PowerEdge M710
server-7 1.0.6 PowerEdge M620
server-9 1.0.5 PowerEdge M520
```

```
racadm getversion
```

```
Bios Version = 2.0.18
iDRAC Version = 2.00.00.00
Lifecycle Controller Version = 2.00.00.00
```

```
racadm getversion -b
```

```
< Server > < BIOS Version > < Blade Type >
server-1 1.6.0 PowerEdge M520
server-2 6.3.0 PowerEdge M610x
server-4 7.0.0 PowerEdge M710HD
server-5 6.3.0 PowerEdge M710
server-7 1.7.1 PowerEdge M620
server-9 1.7.1 PowerEdge M520
```