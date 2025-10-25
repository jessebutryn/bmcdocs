# bioscert

## Description

Allows you to:
- View the installed Secure Boot Certificates. (Login privilege required)
- Export the Secure Boot Certificate to a remote share or local system. (Login privilege required)
- Import the Secure Boot Certificate from a remote share or local system. (Login and system control privilege required)
- Delete the installed Secure Boot Certificate. (Login and system control privilege required)
- Restore the installed Secure Boot Certificate Sections. (Login and system control privilege required)

## Synopsis

- View: `racadm bioscert view –all`
- View specific: `racadm bioscert view -t <keyType> -k <KeySubType> -v <HashValue or ThumbPrintValue>`
- Export: `racadm bioscert export -t <keyType> -k <KeySubType> -v <HashValue or ThumbPrintValue> -f <filename> -l <CIFS/NFS/HTTP/HTTPS share> -u <username> -p <password>`
- Import: `racadm bioscert import -t <keyType> -k <KeySubType> -f <filename> -l <CIFS/NFS/HTTP/HTTPS share> -u <username> -p <password>`
- Delete all: `racadm bioscert delete –all`
- Delete specific: `racadm bioscert delete -t <keyType> -k <KeySubType> -v <HashValue or ThumbPrintValue>`
- Restore all: `racadm bioscert restore –all`
- Restore specific: `racadm bioscert restore -t <keyType>`

## Input

- `-t` — Key type:
  - 0: PK (Platform Key)
  - 1: KEK (Key Exchange Key)
  - 2: DB (Signature Database)
  - 3: DBX (Forbidden signatures Database)
- `-k` — Certificate type or Hash type:
  - 0: Certificate type
  - 1: Hash type (SHA-256)
  - 2: Hash type (SHA-384)
  - 3: Hash type (SHA-512)
- `-v` — Thumbprint value or Hash value
- `-f` — Filename of the exported Secure Boot Certificate
- `-l` — Network location for export/import
- `-u` — Username for remote share
- `-p` — Password for remote share

## Examples

- View all: `racadm bioscert view –all`
- View PK: `racadm bioscert view -t 0 -k 0 -v AB:A8:F8:BD:17:1E:35:12:90:67:CD:0E:69:66:79:9B:BE:64:52:0E`
- Export KEK to CIFS: `racadm bioscert export -t 1 -k 0 -v AB:A8:F8:BD:17:1E:35:12:90:67:CD:0E:69:66:79:9B:BE:64:52:0E -f kek_cert.der -l //10.94.161.103/share -u admin -p mypass`
- Import KEK from CIFS: `racadm bioscert import -t 1 -k 0 -f kek_cert.der -l //10.94.161.103/share -u admin -p mypass`
- Delete all KEK: `racadm bioscert delete --all`
- Restore all: `racadm bioscert restore --all`