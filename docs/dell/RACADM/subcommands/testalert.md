# testalert

## Description

Tests the alert functionality by sending a test alert to configured destinations.

## Synopsis

```bash
racadm testalert -i <alert_index>
```

## Input

- `-i <alert_index>` — Index of the alert destination to test (1-4)

## Output

Sends a test alert to the specified alert destination.

## Example

- Test alert destination 1: `racadm testalert -i 1`