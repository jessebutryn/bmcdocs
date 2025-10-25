# krbkeytabupload

## Description

Uploads a Kerberos keytab file to iDRAC.

To run this subcommand, you must have the Server Control privilege.

## Synopsis

```
racadm krbkeytabupload [-f <filename>]
```

## Input

- `-f` — Specifies the filename of the keytab uploaded. If the file is not specified, the keytab file in the current directory is selected.

## Output/Example

Upload a Kerberos keytab file.

```
racadm krbkeytabupload -f c:\keytab\krbkeytab.tab
```