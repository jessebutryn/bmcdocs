# RACADM Set Command

## Description

The `set` subcommand modifies configuration object values on server components. It supports two forms:

- **Single-object set**: Modify one configuration object via command line
- **Multi-object set**: Modify multiple objects using a configuration file

Supports Server Configuration Profile (SCP) import in XML and JSON formats from local files or network shares (NFS, CIFS, HTTP, HTTPS, FTP, TFTP).

### Application Types

- **Real-time**: Changes applied immediately (iDRAC, Lifecycle Controller, PowerEdge RAID controllers v9.1+)
- **Staged**: Changes applied after system reboot (BIOS, networking devices, some RAID controllers)

### Notes

- Staged changes require job creation and reboot via `jobqueue`
- INI file import/export not supported with `-c` before iDRAC 4.40.00.00
- Some configurations require two imports for full application

## Synopsis

### Single-Object Set

```bash
racadm set <FQDD Alias>.<group> <value>
racadm set <FQDD Alias>.<group>.<object> <value>
racadm set <FQDD Alias>.<group>.[<index>].<object> <value>
racadm set <FQDD Alias>.<index>.<group>.<index>.<object> <value>
```

### Multi-Object Set

```bash
# NFS
racadm set -f <filename> -t xml -l <NFS share> [--preview] [--continue]
racadm set -f <filename> -t xml -l <NFS share> -c <FQDD>[,<FQDD>*]

# CIFS
racadm set -f <filename> -t xml -u <username> -p <password> -l <CIFS share> [--preview] [--continue]
racadm set -f <filename> -t xml -u <username> -p <password> -l <CIFS share> -c <FQDD>[,<FQDD>*]

# FTP/TFTP/HTTP/HTTPS
racadm set -f <filename> -t <type> -u <user> -p <pass> -l <location> [-s <state>] [-c <component_FQDD>] [--preview] [--customdefaults]

# Save custom defaults
racadm set --savecustomdefaults
```

## Input Parameters

- `<FQDD Alias>`: Fully Qualified Device Descriptor (e.g., System.Power, iDRAC.Info)
- `<group>`: Group containing the object
- `<object>`: Object name to modify
- `<index>`: Index for FQDDs or groups
- `<value>`: New value to set
- `-f <filename>`: Configuration file to import
- `-u`: Username for remote share
- `-p`: Password for remote share
- `-l`: Network share location
- `-t`: File type (xml, json)
- `-c`: Specific FQDD(s) to configure
- `--preview`: Validate configuration without applying
- `--customdefaults`: Upload custom default configuration
- `--savecustomdefaults`: Save current config as custom defaults

### Staging and Reboot Options (with -f)
- `-b`: Shutdown type (Graceful, Forced, NoReboot)
- `-w`: Wait time for graceful shutdown (300-3600 seconds, default 1800)
- `-s`: Power state after import (On, Off)

**Notes:**
- `--preview` validates without restarting
- `-b`, `-w`, `-s` only work with `-f`
- Some devices require two imports for complete configuration

## Examples

### Single-Object Set (Real-time)

```bash
# Set LCD display string
racadm set system.lcd.LCDUserString "Server Room A"

# Set iDRAC name
racadm set iDRAC.Info.Name idrac-server100
```

### Single-Object Set (Staged)

```bash
# Configure BIOS settings
racadm set BIOS.SysProfileSettings.ProcTurboMode Disabled
racadm set BIOS.ProcSettings.ProcVirtualization Enabled

# Create job to apply changes and reboot
racadm jobqueue create BIOS.Setup.1-1 -r Graceful

# Check job status
racadm jobqueue view -i <Job_ID>
```

### Multi-Object Set (Real-time)

```bash
# Import from local XML file
racadm set -f myidrac.xml -t xml

# Import from NFS share
racadm set -f config.xml -t xml -l 192.168.1.100:/share

# Import specific component from CIFS
racadm set -f config.xml -t xml -u admin -p pass -l //192.168.0/share -c iDRAC.Embedded.1
```

### Multi-Object Set (Staged)

```bash
# Import with graceful reboot, 10-minute wait, power on after
racadm set -f config.xml -t xml -b Graceful -w 600 -s On

# Import without reboot (manual reboot later)
racadm set -f config.xml -t xml -b NoReboot

# Preview configuration before import
racadm set -f config.xml -t xml -u admin -p pass -l //192.168.0/share --preview
```

### Network Share Examples

```bash
# FTP
racadm set -f config.xml -t xml -u user -p pass -l ftp://192.168.10.24/

# TFTP
racadm set -f config.xml -t xml -l tftp://192.168.10.24/

# HTTP
racadm set -f config.xml -t xml -u user -p pass -l http://example.com/share

# HTTPS
racadm set -f config.json -t json -u user -p pass -l https://example.com/share
```

### Custom Defaults

```bash
# Save current configuration as custom defaults
racadm set --savecustomdefaults

# Upload custom defaults from NFS
racadm set -f defaults.xml -t xml -l 192.168.1.100:/share --customdefaults
```

For more information, run `racadm help set`.