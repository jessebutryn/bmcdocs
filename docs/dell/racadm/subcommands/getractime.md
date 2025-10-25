# getractime

## Description

Displays the current iDRAC time.

## Synopsis

```bash
racadm getractime [-d]
```

## Input

- `-d` — Displays the time in the format, YYYYMMDDhhmmss.

## Output

The current iDRAC time is displayed.

## Example

```bash
racadm getractime
```

Output:

```
Mon May 13 17:17:12 2013
```

```bash
racadm getractime -d
```

Output:

```
20141126114423
```