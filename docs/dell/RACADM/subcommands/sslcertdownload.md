# sslcertdownload

## Description

Downloads an SSL certificate from iDRAC to the client's file system.

To run this subcommand for web server certificates, you must have Login to iDRAC and Configure iDRAC privileges and for others only Control and Configure System privilege is required.

NOTE: This subcommand is only supported on the remote interface(s).

## Synopsis

```
racadm sslcertdownload -f <filename> -t <type>
racadm sslcertdownload -t 8 -i <instance(1 or 2)>
```

## Input

- `-f` — Specifies the target filename on local file system to download the certificate.
- `-t <type>` — Specifies the type of certificate to download, either the CA certificate for Directory Service or the server certificate.
  - 1 — Server Certificate
  - 2 — Active Directory
  - 3 — Custom Signing Certificate
  - 4 — Client Trust Certificate for SSL
  - 6 — SEKM SSL certificate
  - 7 — KMS CA certificate
  - 8 — Rsyslog Server CA
  - 9 — RSA CA certificate
  - 10 — SCEP CA certificate
  - 11 — SCV Signed Certificate
  NOTE: This input is available for local RACADM only.
  - 16 — Custom certificate

## Output/Example

Download server certificate:

```
racadm -r 192.168.0 -u root -p xxx sslcertdownload -t 1 -f cert.txt
```

Download Active Directory certificate:

```
racadm -r 192.168.0 -u root -p xxx sslcertdownload -t 2 -f ad_cert.txt
```

Download telemetry certificate:

```
racadm -r 192.168.0 -u root -p xxx sslcertdownload -t 8 -i 1
```

NOTE: This command is not supported in the firmware RACADM interface as it is not a file system.