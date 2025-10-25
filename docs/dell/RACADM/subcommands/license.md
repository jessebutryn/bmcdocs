# license

## Description

Manages the hardware licenses.

## Synopsis

```bash
racadm license view [-c <component>]
racadm license import [-f <licensefile>] -l <location> -u <username> -p <password> -c <component> [-o]
racadm license import -u <username> -p <password> -f <license file name> -l <location> -c <FQDD> [-o]
racadm license export -f <license file> [-l <location>] [-u <username>] [-p <password>] -e <ID> -c <component>
racadm license export -u <username> -p <password> -f <license file name> -l <location> -t <transaction ID>
racadm license export -u <username> -p <password> -f <license file name> -l <locaton> -e <entitlement ID>
racadm license export -u <username> -p <password> -f <license file name> -l <location> -c <FQDD>
racadm license delete -t <transaction ID> [-o]
racadm license delete -e <entitlement ID> [-o]
racadm license delete -c <component> [-o]
```

## Input

- view — View license information.
- import — Installs a new license.
- export — Exports a license file.
- delete — Deletes a license from the system.
- `-l <remote share location>` — Network share location from where the license file must be imported. Possible locations are NFS, CIFS, HTTP, HTTPS, FTP, TFTP.
  - If the file is on a shared location, then -u <share user> and -p <share password> must be used.
  - NOTE: Using an invalid or unreachable IP for remote share (HTTP, HTTPS, FTP, TFTP) may not return an error message.
- `-f` — Filename or path to the license file
- `-e <ID>` — Specifies the entitlement ID of the license file that must be exported
- `-t <ID>` — Specifies the transaction ID.
- `-c <component>` — Specifies the component name on which the license is installed.
- `-o` — Overrides the End User License Agreement (EULA) warning and imports, replaces or deletes the license.
- `-u` — Username of the system where the file will be exported.
- `-p` — Password of the user on the system where the file will be exported.

NOTE: Only a user with Server Control and Configure iDRAC privilege can run the import, delete, and replace commands.

NOTE: For export license, you need Login and Configure iDRAC privilege.

NOTE: This command supports both IPV4 and IPV6 formats. IPV6 is applicable for CIFS and NFS type remote shares.

## Examples

- View all License Information on System.
  ```bash
  racadm license view
  ```
  Output:
  ```
  iDRAC.Embedded.1
  Status = OK
  Device = iDRAC.Embedded.1
  Device Description = iDRAC
  Unique Identifier = H1VGF2S
  ```