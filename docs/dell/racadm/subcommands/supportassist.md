# supportassist

## Description

Allows you to perform supportassist operations such as:

- collect: Collects the supportassist data and exports to local share, or remote share, or Dell site depending on the parameters given in the command.
- register: Allows registration of supportassist to enable related features.
- exportlastcollection: Exports the last collected supportassist data to the share which is mentioned in the command or to the default share.
- accepteula: Accepts the End User License Agreement (EULA).
- geteulastatus: Provides the status of the End User License Agreement (EULA).
- uploadlastcollection: Upload last collection to Dell supportassist server.
- exposeisminstallertohostos: Exposes iSM installer to host OS, so that user can install the iSM from host side.
- autocollectscheduler: Provides options to create view, and clear the time-based automatic collections.

## Synopsis

```
racadm supportassist <support assist command type>
racadm supportassist collect [-t <logtype>]
racadm supportassist collect [-t <logtype>] -upload
racadm supportassist collect [-t <logtype>] -l <CIFS or NFS share> -u <username> -p <password>
racadm supportassist collect [-t <logtype>] -l <CIFS or NFS share> -u <username> -p <password> --upload
racadm supportassist collect -f <filename>
racadm supportassist exportlastcollection -l <CIFS/NFS/TFTP/FTP/HTTP/HTTPS share> -u myuser -p mypass
racadm supportassist exportlastcollection
racadm supportassist accepteula
racadm supportassist geteulastatus
racadm supportassist register -pfname <primary first name> -plname <primary last name> -pmnumber <primary number> -panumber <primary alternate number> -pmailid <primary email id> -sfname <secondary first name> -slname <secondary last name> -smnumber <secondary number> -sanumber <secondary alternate number> -smailid <secondary email id> -company <company name> -street1 <street1 name> -street2 <street2 name> -city <city name> -state <state name> -country <country name> -zip <zip or postal code>
racadm supportassist uploadlastcollection
racadm supportassist exposeisminstallertohostos
```

## Input

- `-t` — Type of logs. You can specify any of the following values that are separated by a ',' (comma): SysInfo, OSAppNoPII, OSAppAll, TTYLog
- `-l` — Network share location to export the report
- `-u` — User name for the remote share to export the report
- `-p` — Password for the remote share to export the report
- `-f` — Target filename for the exported log (must have .zip extension)
- `-pfname` — Specifies the primary user's first name
- `-plname` — Specifies the primary user's last name
- `-pmnumber` — Specifies the primary user's number
- `-panumber` — Specifies the primary user's alternate number
- `-pmailid` — Specifies the primary user's email address
- `-sfname` — Specifies the secondary user's first name
- `-slname` — Specifies the secondary user's last name
- `-smnumber` — Specifies the secondary user's number
- `-sanumber` — Specifies the secondary user's alternate number
- `-smailid` — Specifies the secondary user's email address
- `-company` — Specifies the company name
- `-street1` — Specifies the street address of the company
- `-street2` — Specifies the secondary street address of the company
- `-city` — Specifies the name of the city
- `-state` — Specifies the name of the state
- `-country` — Specifies the name of the country
- `-zip` — Specifies the zip or postal code

## Output/Example

Collect the system information data.

```
racadm supportassist collect
```

Collect the filtered data.

```
racadm supportassist collect --filter
```

Collect the data and export to an FTP share.

```
racadm supportassist collect -t Debug -l ftp://192.168.10.24/share -u myuser -p mypass
```

Collect the data and export to a TFTP share.

```
racadm supportassist collect -t Debug -l tftp://192.168.10.24/share
```

Collect the data and export to a CIFS share.

```
racadm supportassist collect -t sysinfo -l //192.168.10.24/share -u myuser -p mypass
```

Collect the data and export to an HTTP share.

```
racadm supportassist collect -t TTYLog -l http://192.168.10.24/share -u myuser -p mypass
```

Collect the data and export to an HTTPS share.

```
racadm supportassist collect -t Debug -l https://192.168.10.24/share -u myuser -p mypass
```

Export the last collected supportassist data to an FTP share.

```
racadm supportassist exportlastcollection -l ftp://192.168.10.24/share -u myuser -p mypass
```

Export the collected supportassist data to the default network share.

```
racadm supportassist exportlastcollection
```

Accept the End User License Agreement (EULA).

```
racadm supportassist accepteula
```

Check the End User License Agreement (EULA) status.

```
racadm supportassist geteulastatus
```

Register the iDRAC for supportassist features.

```
racadm supportassist register -pfname abc -plname xyz -pmnumber 1234567890 -panumber 1234567899 -pmailid abc_xyz@Dell.com -sfname abc -slname xyz -smnumber 1234567890 -sanumber 7777799999 -smailid abc_xyz@dell.com -company dell -street1 xyztechpark -street2 -city bangalore -state karnataka -country india -zip 123456
```

Upload the last collection to the Dell supportassist server.

```
racadm supportassist uploadlastcollection
```

Expose the iSM installer to the host operating system for the iSM installation.

```
racadm supportassist exposeisminstallertohostos
```