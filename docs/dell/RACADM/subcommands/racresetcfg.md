# racresetcfg

## Description

Deletes your current iDRAC configuration and resets iDRAC to the factory default settings based on the options provided.

If you run racresetcfg from a network client for example, a supported web browser, SSH, or Remote RACADM), use the default IP address which is 192.168.0.120. The racresetcfg subcommand does not reset the cfgDNSRacName object.

To run this subcommand, you must have the Configure iDRAC privilege and Configure User privilege.

NOTE: Certain firmware processes must be stopped and restarted to complete the reset to defaults. iDRAC becomes unresponsive for about 30 seconds while this operation completes.

## Synopsis

- RAC reset operation initiated successfully. It may take several minutes for the RAC to come online again.

```
racadm racresetcfg
racadm racresetcfg -f
racadm racresetcfg [-all]
racadm racresetcfg [-rc]
```

## Input

- `-f` — Force racresetcfg. If any vFlash partition creation or formatting is in progress, iDRAC returns a warning message. You can perform a force reset using this option.
- `-all` — Discard all settings and reset user to shipping value.
- `-rc` — Discard all settings and reset user to default user name and password.

NOTE: When you perform racresetcfg -rc on Stomp and Noble/VRTX servers, by default, the DHCP is disabled.

## Output/Example

Reset the configuration on iDRAC.

```
racadm racresetcfg
```

The RAC configuration has initiated restoration to factory defaults. Wait up to a minute for this process to complete before accessing the RAC again.

Reset when vFlash partition creation is in progress.

```
racadm racresetcfg
```

A vFlash SD card partition operation is in progress. Resetting the iDRAC may corrupt the vFlash SD card. To force racresetcfg, use the -f flag.

Reset all iDRAC's configurations to default, and preserve the user and network settings.

```
racadm racresetcfg -f
```

Reset all iDRAC's configurations to default, and reset the user to shipping value.

```
racadm racresetcfg -all
```

Reset all iDRAC's configurations to default, and reset the user to root/calvin.

```
racadm racresetcfg -rc
```