# SetUsbAccessMode

Dynamically controls USB port access mode (in-band only).

## Syntax

```
sum -c SetUsbAccessMode --panel <front/rear> --disable
sum -c SetUsbAccessMode --panel <front/rear> --enable
```

## Options

- `--panel <front/rear>`: Specifies which panel's USB ports to control.
- `--disable`: Disables the USB port access.
- `--enable`: Enables the USB port access.

## Examples

### Disable Front Panel USB
```
[SUM_HOME]# ./sum -c SetUsbAccessMode --panel front --disable
```

### Enable Front Panel USB
```
[SUM_HOME]# ./sum -c SetUsbAccessMode --panel front --enable
```

### Disable Rear Panel USB
```
[SUM_HOME]# ./sum -c SetUsbAccessMode --panel rear --disable
```

### Enable Rear Panel USB
```
[SUM_HOME]# ./sum -c SetUsbAccessMode --panel rear --enable
```

## Notes

- Only when "Front USB Port(s)" or "Rear USB Port(s)" is set to "Enabled (Dynamic)" in the BIOS configurations is the command "SetUsbAccessMode" allowed to dynamically enable/disable the USB port access mode.
- For some systems, a plugged-in USB 3.0 device cannot be used after the port is dynamically disabled and enabled again. When the device cannot be used after the port is dynamically enabled, SUM will output a message "USB 3.0 device may need to be manually unplugged and plugged for use" to bring this to the user's attention.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/setusbaccessmode.md