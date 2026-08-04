# SetUsbAccessMode

Dynamically enables or disables the USB ports on the front or rear panel in the running operating system. In-band only.

## Syntax

### In-Band
```
saa -c SetUsbAccessMode --panel <front|rear> {--disable | --enable}
```

## Options

- `--panel <front/rear>`: The panel to be set.
- `--enable`: Dynamically enables the USB ports in the assigned panel.
- `--disable <front/rear>`: Dynamically disables the USB ports in the assigned panel.

## Examples

### In-Band
```bash
[SAA_HOME]# ./saa -c SetUsbAccessMode --panel front --disable
```

## Output

```
[USB access mode]
REAR panel....................dynamic enabled
FRONT panel...................static disabled
```

```
[USB access mode]
FRONT panel....................dynamic disabled
```

## Notes

- This command is only allowed when "Front USB Port(s)" or "Rear USB Port(s)" is set to "Enabled (Dynamic)" in the BIOS configuration.
- For some systems, a plugged-in USB 3.0 device cannot be used after the port is dynamically disabled and then re-enabled. When this happens, SAA outputs the message "USB 3.0 device may need to be manually unplugged and plugged for use."
