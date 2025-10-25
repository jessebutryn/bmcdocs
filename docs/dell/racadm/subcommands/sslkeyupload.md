# sslkeyupload

## Description

Uploads SSL key from the client to iDRAC.

To run this subcommand, you must have the Server Control privilege.

## Synopsis

```
racadm sslkeyupload -t <type> -f <filename>
```

## Input

- `-t` — Specifies the key to upload. The value is:
  - 1 — SSL key used to generate the server certificate.
- `-f` — Specifies the filename of the SSL key that must be uploaded.

## Output/Example

If upload is successful, the message SSL key successfully uploaded to the RAC is displayed. if upload is unsuccessful, error message is displayed.

```
racadm sslkeyupload -t 1 -f c:\sslkey.txt
```