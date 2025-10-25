# setled

## Description

Sets the state (blinking or not blinking) of the LED on the specified module.

To run this subcommand, you must have the Configure iDRAC permission.

## Synopsis

```
racadm setled -l <ledState>
```

## Input

- `-l <ledState>` — Specifies the LED state. The values are:
  - 0 — No Blinking
  - 1 — Blinking

## Output/Example

Stop LED from blinking.

```
racadm setled -l 0
RAC0908: System ID LED blink off.
```

Start LED to blink.

```
racadm setled -l 1
RAC0907: System ID LED blink on.
```