# GetUsbAccessMode

Gets the USB port access mode (front and rear panel) in the running operating system. In-band only.

## Syntax

### In-Band
```
saa -c GetUsbAccessMode
```

## Options

None.

## Examples

### In-Band
```bash
[SAA_HOME]# ./saa -c GetUsbAccessMode
```

## Output

```
[USB access mode]
REAR panel....................dynamic enabled
FRONT panel...................static disabled
```

## Notes

- SAA currently does not support USB port accessibility control for AMD platforms.
- There are four USB port access modes: Dynamically Enabled, Dynamically Disabled, Statically Enabled, and Statically Disabled.
- Front panel refers to USB ports connected to a 19-pin USB header on the motherboard; rear panel refers to the built-in USB ports on the motherboard.
- USB port accessibility is configured by the BIOS settings "Front USB Port(s)" and "Rear USB Port(s)" during POST. Only ports set to "Enabled (Dynamically)" can be switched at runtime with `SetUsbAccessMode`.
