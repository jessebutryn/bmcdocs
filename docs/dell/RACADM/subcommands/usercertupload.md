# usercertupload

## Description

Uploads a user certificate or a user CA certificate from the client to iDRAC.

To run this subcommand, you must have the Configure iDRAC permission.

## Synopsis

```
racadm usercertupload -t <type> [-f <filename>] -i <index>
```

## Input

- `-t` — Specifies the type of certificate to upload, either the CA certificate or server certificate.
  - 1 = user certificate
  - 2 = user CA certificate
- `-f` — Specifies the filename of the certificate that must be uploaded. If the file is not specified, the sslcert file in the current directory is selected.
- `-i` — Index number of the user. Valid values 2–16.

## Output/Example

Upload user certificate for user 6.

```
racadm usercertupload -t 1 -f c:\cert\cert.txt -i 6
```