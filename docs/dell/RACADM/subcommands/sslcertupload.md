# sslcertupload

## Description

Uploads a custom SSL server or CA certificate for Directory Service from the client to iDRAC.

To run this subcommand, you must have the following privilege:

- Active Directory certificate - Configure iDRAC and Configure Users.
- Public Key Cryptography Standards (PKCS) format - Configure iDRAC.
- Client Trust certificate for SSL format - Configure iDRAC
- Web server certificate- Login to iDRAC and Configure iDRAC

NOTE: For this command, files without extension or no extension are allowed.

## Synopsis

```
racadm sslcertupload -t <type> -f <filename> -p <passphrase>
racadm sslcertupload -t 8 -i <instance(1 or 2)>
```

## Input

- `-f` — Specifies the source filename in the local file system of the certificate uploaded.
- `-p` — Pass phrase for the Public Key Cryptography Standards file.
- `-t` — Specifies the type of certificate to upload. The type of certificate must be:
  - 1 — Server certificate
  - 2 — CA certificate for Directory Service
  - 3 — Public Key Cryptography Standards (PKCS) format
  - 4 — Client Trust certificate for SSL format
  - 6 — SEKM SSL certificate
  - 7 — KMS CA certificate
  - 8 — Rsyslog Server CA
  - 9 — RSA CA certificate
  - 10 — SCEP CA certificate
  - 16 — Custom certificate
- `-i` — Instance value. This is applicable only for Rsyslog Server CA certificate.

## Output/Example

Uploading a server certificate:

```
racadm -r 192.168.0.2 -u root -p xxx sslcertupload -t 1 -f cert.txt
```

Uploading web server certificate and key:

```
racadm -r 192.168.0.2 -u root -p xxx sslcertupload -t 6 -f cert.txt -k key.txt
```

Uploading Active Directory certificate:

```
racadm -r 192.168.0.2 -u root -p xxx sslcertupload -t 2 -f ad_cert.txt
```

Uploading Client Trust certificate for SSL:

```
racadm -r 192.168.0.2 -u root -p xxx sslcertupload -t 4 -f https_cert.cer
```

Uploading a telemetry certificate:

```
racadm -r 192.168.0.2 -u root -p xxx sslcertupload -t 8 -i 1
```