# usercertview

## Description

Displays the user certificate or the user CA certificate.

## Synopsis

```
racadm usercertview -t <type> [-A] -i <index>
```

## Input

- `-t` — Specifies the type of certificate to view, either the user certificate or the user CA certificate.
  - 1 = user certificate
  - 2 = user CA certificate
- `-A` — Prevents printing headers or labels.
- `-i` — Index number of the user. Valid values are 2–16.

## Output/Example

To view user certificate for user 6.

```
racadm usercertview -t 1 -i 6
```

```
Serial Number: 01
Subject Information:
Country Code (CC)
State (S)
Locality (L)
Organization (O)
Common Name (CN): US
: Texas
: Round Rock
: Dell Inc.
: iDRAC default certificate
Issuer Information:
Country Code (CC)
: US
State (S)
: Texas
Locality (L)
: Round Rock
Organization (O)
: Dell Inc.
Organizational Unit (OU): Remote Access Group
Common Name (CN)
: iDRAC default certificate
Valid From
Valid To
: May 7 23:54:19 2017 GMT
: May 4 23:54:19 2027 GMT
```