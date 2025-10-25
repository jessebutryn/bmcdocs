# sslcertview

## Description

Displays the SSL server or CA certificate that exists on iDRAC.

## Synopsis

```
racadm sslcertview -t <type> [-A]
racadm sslcertview -t <type> -i <instance>
```

## Input

- `-t` — Specifies the type of certificate to view:
  - 1 — Server Certificate
  - 2 — Active Directory
  - 4 — Client Trust certificate for SSL
  - 6 — SEKM SSL certificate
  - 7 — KMS CA certificate
  - 8 — Rsyslog CA certificate
  - 9 — RSA CA certificate
  - 10 — SCEP CA certificate
- `-A` — Prevents printing headers or labels.
- `-i` — Instance value should be 1 or 2. This is applicable only for Rsyslog Server CA certificate (-t 8)

NOTE: If a certificate is generated using a comma ',' as one of the parameters, command displays the partial name in the following fields only until the comma:

- Organization Name
- Common Name
- Location Name
- State Name

The rest of the string is not displayed.

## Output/Example

```
racadm sslcertview -t 1
```

```
Serial Number
Subject Information:
Country Code (CC)
State (S)
Locality (L)
Organization (O)
Organizational Unit (OU)
Common Name (CN)
Issuer Information:
Country Code (CC)
State (S)
Locality (L)
Organization (O)
Organizational Unit (OU)
Common Name (CN)
Valid From
Valid To
01
US
Texas
Round Rock
Dell Inc.
Remote Access Group
iDRAC Default certificate
US
Texas
Round Rock
Dell Inc.
Remote Access Group
iDRAC Default certificate
May 15 23:54:19 2017 GMT
May 12 23:54:19 2027 GMT
```

```
racadm sslcertview -t 1 -A
```

```
00
US
Texas
Round Rock
Dell Inc.
Remote Access Group
iDRAC default certificate
US
Texas
Round Rock
Dell Inc.
Remote Access Group
iDRAC default certificate
May 15 23:54:19 2017 GMT
May 12 23:54:19 2027 GMT
```

To view the server certificate:

```
racadm -r 192.168.0.2 -u root -p xxx sslcertview -t 1
```

```
racadm -r 192.168.0.2 -u root -p xxx sslcertview -t 8 -i 1
```

To view the server certificate with headers and labels omitted:

```
racadm -r 192.168.0.2 -u root -p xxx sslcertview -t 1 -A
```

```
racadm -r 192.168.0.2 -u root -p xxx sslcertview -t 8 -i 1 -A
```