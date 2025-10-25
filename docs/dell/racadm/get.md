# RACADM Get Command

## Description

The `get` subcommand displays the value of one or more objects. It supports two forms:

- **Single-object get**: Displays the value of a single object
- **Multi-object get**: Exports the value of multiple objects to a file

Supports Server Configuration Profile (SCP) export in XML and JSON formats to local files or network shares (NFS, CIFS, HTTP, HTTPS, FTP, TFTP).

### Notes

- Some objects may have pending values requiring job completion via `jobqueue`
- INI file import/export not supported with `-c` option before iDRAC 4.40.00.00
- Autobackup returns license error on Rx4xx/Mx4xx platforms from iDRAC 4.40.00.00

## Synopsis

### Single-Object Get

```bash
racadm get <FQDD Alias>.<group>
racadm get <FQDD Alias>.<group>.<object>
racadm get <FQDD Alias>.<group>.[<index>].<object>
racadm get <FQDD Alias>.<index>.<group>.<index>.<object>
```

### Multi-Object Get

```bash
# NFS
racadm get -f <filename> -t xml -l <NFS share> [--clone | --replace] [--includeph]
racadm get -f <filename> -t xml -l <NFS share> -c <FQDD>[,<FQDD>*]

# FTP
racadm get -f <filename> -t xml -u <username> -p <password> -l <FTP share> -c <FQDD>

# TFTP
racadm get -f <filename> -t xml -l <TFTP share> -c <FQDD>

# CIFS
racadm get -f <filename> -t xml -u <username> -p <password> -l <CIFS share> [--clone | --replace] [--includeph]
racadm get -f <filename> -t xml -u <username> -p <password> -l <CIFS share> -c <FQDD>[,<FQDD>*]

# HTTP/HTTPS
racadm get -f <filename> -t xml -u <username> -p <password> -l <HTTP/HTTPS share> -c <FQDD>

# Custom defaults
racadm get -f <filename> -t xml --customdefaults

# With telemetry
racadm get -f -t xml -l <share> -u <username> -p <password> [--includeCustomTelemetry]
```

## Input Parameters

- `<FQDD Alias>`: Fully Qualified Device Descriptor (e.g., System.Power, iDRAC.Serial)
- `<group>`: Group containing the object
- `<object>`: Object name to read
- `<index>`: Index for FQDDs or groups
- `-f <filename>`: Export filename
- `-u`: Username for remote share
- `-p`: Password for remote share
- `-l`: Network share location
- `-t`: File type (xml, json)
- `--clone`: Export without system-specific details
- `--replace`: Export with system-specific details
- `-c`: Specific FQDD(s) to export
- `--includeph`: Include passwords in hashed format
- `--customdefaults`: Export custom default configuration
- `--includeCustomTelemetry`: Include telemetry metrics

**Proxy Configuration**: For HTTP/HTTPS operations, configure proxy via `lifecyclecontroller.lcattributes` (UserProxyUserName, UserProxyPassword, etc.)

## Examples

### Single Object
```bash
# Get LCD user string
racadm get system.lcd.LCDUserString

# Get topology configuration
racadm get system.location

# Get rack name
racadm get system.location.rack.name
```

### Multi-Object Export
```bash
# Export to CIFS
racadm get -f config.xml -t xml -u admin -p pass -l //192.168.0/share

# Export to NFS
racadm get -f config.xml -t xml -l 192.168.0.1:/share

# Clone configuration
racadm get -f clone.xml -t xml -u admin -p pass -l //192.168.0/share --clone

# Export specific component
racadm get -f idrac.xml -t xml -u admin -p pass -l //192.168.0/share -c iDRAC.Embedded.1

# Export to FTP
racadm get -f config.xml -t xml -u user -p pass -l ftp://192.168.10.24/

# Export JSON to HTTP
racadm get -f config.json -t json -u user -p pass -l http://example.com/share

# Include password hashes
racadm get -f config.xml -t xml -l //share --includeph

# Custom defaults
racadm get -f defaults.xml -t xml --customdefaults

# With telemetry
racadm get -f config.xml -t xml -l //share -u user -p pass --includeCustomTelemetry
```

### Proxy Setup
```bash
# Configure proxy
racadm set lifecyclecontroller.lcattributes.UserProxyUsername proxyuser
racadm set lifecyclecontroller.lcattributes.UserProxyPassword proxypass
racadm set lifecyclecontroller.lcattributes.UserProxyServer proxy.example.com
racadm set lifecyclecontroller.lcattributes.UserProxyPort 8080
racadm set lifecyclecontroller.lcattributes.UserProxyType http

# View proxy settings
racadm get lifecycleController.lcAttributes
```

For more information, run `racadm help get`.