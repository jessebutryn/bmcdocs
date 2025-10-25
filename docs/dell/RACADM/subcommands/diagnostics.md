# diagnostics

## Description

Collects and exports remote diagnostics report from iDRAC. The results of the latest successfully run remote diagnostics are available and retrievable remotely through NFS, CIFS, HTTP, or HTTPS share.

## Synopsis

- Run diagnostics: `racadm diagnostics run -m <mode> -r <reboot type> -s <start time> -e <expiration time>`
- Export diagnostics: `racadm diagnostics export -f <filename> -l <share location> -u <username> -p <password>`

## Input

- `-m <mode>` — Diagnostic mode:
  - 0: Express (subset of tests)
  - 1: Extended (all tests)
  - 2: Both (express and extended serially)
- `-f <filename>` — Name of the configuration file
- `-l` — Network share location (NFS, CIFS, HTTP, HTTPS)
- `-u <username>` — Username for remote share
- `-p <password>` — Password for remote share
- `-r <reboot type>` — Reboot type:
  - pwrcycle: Power cycle
  - graceful: Graceful reboot without forced shutdown
  - forced: Graceful reboot with forced shutdown
- `-s <start time>` — Start time in yyyymmddhhmmss format (default: TIME_NOW)
- `-e <expiration time>` — Expiry time in yyyymmddhhmmss format (default: TIME_NA)

**Note:** Time difference between -s and -e must be more than 5 minutes.

## Output

Provides the Job ID for the diagnostic operation.

## Examples

- Run extended diagnostics with forced reboot: `racadm diagnostics run -m 1 -r forced -s 20121215101010 -e TIME_NA`
- Export to CIFS: `racadm diagnostics export -f diagnostics -l //192.168.0/cifs -u administrator -p xxx`
- Export to NFS: `racadm diagnostics export -f diagnostics -l 192.168.0:/nfs -u administrator -p xxx`
- Export to HTTP: `racadm diagnostics export -f diags.txt -u httpuser -p httppwd -l http://test.com`
- Export to local: `racadm diagnostics export -f diags.txt`