# sslcertdelete

## Description

Command to delete a custom signing certificate from iDRAC.

To run this subcommand for web server certificates, you must have Login to iDRAC and Configure iDRAC privileges and for others only Configure iDRAC privilege is required.

## Synopsis

```
racadm sslcertdelete -t <type>
racadm sslcertdelete -t 8 -i <instance(1 or 2)>
```

## Input

- `-t` — Specifies the type of certificate to delete. The type of certificate is:
  - 3 — Custom signing certificate
  - 4 — Client trust certificate for SSL
  - 8 — Telemetry certificate

## Output/Example

Use Remote RACADM to delete the custom signing certificate.

```
$ racadm -r 192.168.0 -u root -p xxx sslcertdelete -t 3
```

Use Remote RACADM to delete the Client Trust certificate for SSL.

```
$ racadm -r 192.168.0 -u root -p xxx sslcertdelete -t 4
```

Use Remote RACADM to delete the telemetry certificate.

```
racadm -r 192.168.0 -u root -p xxx sslcertdelete -t 8 -i 1
```