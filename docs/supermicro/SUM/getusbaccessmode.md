# GetUsbAccessMode

## Description

Use the inband command "GetUsbAccessMode" to get USB access mode in the running operating system. Currently, SUM supports dynamically disabling/enabling both front and rear panel USB ports. There are four USB port access modes:

- Dynamically Enabled: A USB port is dynamically enabled.
- Dynamically Disabled: A USB port is dynamically disabled.
- Statically Enabled: A USB port is enabled by BIOS during POST, and it cannot be dynamically disabled in the running operating system.
- Statically Disabled: A USB port is disabled by BIOS during POST, and it cannot be dynamically enabled in the running operating system.

## Syntax

```
sum -c GetUsbAccessMode
```

## Options

None.

## Examples

### In-Band
```
[SUM_HOME]# ./sum -c GetUsbAccessMode
The console output contains the following information.
[USB access mode]
REAR panel....................dynamic enabled
FRONT panel...................static disabled
```
