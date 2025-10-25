# sslcsrgen

## Description

Generates and downloads a certificate signing request (CSR) file to the client's local file system. The CSR can be used for creating a custom SSL certificate that can be used for SSL transactions on iDRAC.

To run this subcommand, you must have the Configure iDRAC privilege.

## Synopsis

```
racadm sslcsrgen -g
racadm sslcsrgen [-g] [-f <filename>]
racadm sslcsrgen -s
racadm sslcsrgen –g -t <csr_type>
racadm sslcsrgen -g -f <filename> -t <csr_type>
racadm sslcsrgen -s -t <csr_type>
```

## Input

- `-g` — Generates a new CSR.
- `-s` — Returns the status of a CSR generation process (generation in progress, active, or none).
- `-f` — Specifies the filename of the location, <filename>, where the CSR is downloaded.
  NOTE: The -f option is only supported on the remote interfaces.
- `-t` — Specifies the type of CSR to be generated. The options are:
  - 1 — SSL cert

## Output/Example

If no options are specified, a CSR is generated and downloaded to the local file system as sslcsr by default. The -g option cannot be used with the -s option, and the -f option can only be used with the -g option.

The sslcsrgen -s subcommand returns one of the following status codes:

- CSR was generated successfully.
- CSR does not exist.

Display the status of CSR operation:

```
racadm sslcsrgen -s
```

Generate and download a CSR to local file system using remote RACADM

```
racadm -r 192.168.0.120 -u <username> -p <password> sslcsrgen -g -f csrtest.txt
```

Generate and download a CSR to local file system using local RACADM

```
racadm sslcsrgen -g -f c:\csr\csrtest.txt
```

NOTE: Before a CSR can be generated, the CSR fields must be configured in the RACADM iDRAC.Security group. For example:

```
racadm set iDRAC.security.commonname MyCompany
```

NOTE: In or SSH console, you can only generate and not download the CSR file.