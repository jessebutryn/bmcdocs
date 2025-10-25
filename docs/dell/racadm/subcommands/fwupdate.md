# fwupdate

## Description

Allows you to update the firmware. You can:
- Check the firmware update process status
- Update iDRAC firmware from FTP or TFTP server
- Update iDRAC firmware from the local file system
- Roll back to the standby firmware

To use this subcommand, you must have Configure iDRAC permission.

**Notes:**
- This command is only for iDRAC firmware update. For BIOS or DUPs, use `update` subcommand
- If iSM is exposed on host, you may see "Firmware update operation is already in progress" error

## Synopsis

- Status: `racadm fwupdate -s`
- Update from TFTP: `racadm fwupdate -g -u -a <TFTP_Server_IP_Address> [-d <path>] [--clearcfg]`
- Update from FTP (remote): `racadm -r <iDRAC IP_Address> -u <username> -p <password> fwupdate -f <ftpserver ip> <ftpserver username> <ftpserver password> -d <path>`
- Rollback: `racadm fwupdate -r`
- Upload from local: `racadm fwupdate -p -u [-d <path>]`

## Input

- `-u` — Update option: performs checksum and starts update process
- `-s` — Returns status of update process
- `-a` — TFTP server IP address (used with -g)
- `--clearcfg` — Removes previous iDRAC configuration after update
- `-g` — Get firmware from TFTP server (use with -a, -u, -d)
- `-p` — Put/upload firmware file from managed system to iDRAC
- `-d <path>` — Path to firmware file (default: TFTP directory)
- `-r` — Rollback to standby firmware

**Notes:**
- Firmware image path length cannot exceed 256 characters
- Filename must be `firmimgFIT.d9` for FTP/TFTP
- `-p` option not supported on serial/ssh console and Linux OS

## Output

Displays message indicating the operation being performed.

## Examples

- Upload from client and update: `racadm fwupdate -p -u -d /tmp/images`
- Update from FTP: `racadm fwupdate -f 192.168.0.10 test test -d firmimgFIT.d9`
- Update from TFTP: `racadm fwupdate -g -u -a 192.168.0.100 -d /tmp/images`
- Check status: `racadm fwupdate -s`
- Rollback: `racadm fwupdate -r`
- Update with config clear: `racadm fwupdate -g -u -a 192.168.0.100 -d /tmp/images --clearcfg`