# httpsbootcert

## Description

Allows you to manage BIOS https Boot Certificate Management operations.

## Synopsis

- To import the bios https Boot Certificate from a remote share or local system

```
racadm httpsbootcert help import
```

- To export the bios https boot Certificate to a remote share or local system

```
racadm httpsbootcert help export
```

- To delete the bios https boot certificate

```
racadm httpsbootcert help delete
```

## Input

- `-i` — Index of the boot device 1 to 4
- `-f` — Filename of the bios https Boot Device Certificate
- `-l` — Network share location <CIFS/NFS/HTTP/HTTPS share>
- `-u` — Username for the remote share
- `-p` — Password for the remote share

NOTE: The supported file formats are .cer,.der,.crt,.pem and .txt.

NOTE: This command supports both IPV4 and IPV6 formats. IPV6 is applicable for CIFS and NFS type remote shares.

## Output/Example

To import the boot device cert with index 1 from a remote CIFS share:

```
racadm httpsbootcert import -i 1 -f httpsboot_cert.txt -l //10.94.161.103/share -u admin -p mypass
```

To import the boot device cert with index 2 from a remote NFS share:

```
racadm httpsbootcert import -i 2 -f httpsboot_cert.cer -l 192.168.2.14:/share
```

To import the boot device cert with index 2 from a remote HTTP share:

```
racadm httpsbootcert import -i 2 -f httpsboot_cert.der -l http://192.168.10.24/share -u myuser -p mypass
```

To import the boot device cert with index 2 from a remote HTTPS share:

```
racadm httpsbootcert import -i 2 -f httpsboot_cert.pem -l https://192.168.10.24/share -u myuser -p mypass
```

To import the boot device cert with index 3 from a local share using local racadm:

```
racadm httpsbootcert import -f httpsboot_cert.crt
```

To import the boot device cert with index 4 from a local share using remote racadm:

```
racadm -r 10.94.161.119 -u root -p calvin httpsbootcert import -f httpsboot_cert.txt
```

To export the boot device cert with index 1 to a remote CIFS share:

```
racadm httpsbootcert export -i 1 -f httpsboot_cert.txt -l //10.94.161.103/share -u admin -p mypass
```

To export the boot device cert with index 2 to a remote NFS share:

```
racadm httpsbootcert export -i 2 -f httpsboot_cert.cer -l 192.168.2.14:/share
```

To export the boot device cert with index 2 to a remote HTTP share:

```
racadm httpsbootcert export -i 2 -f httpsboot_cert.der -l http://192.168.10.24/share -u myuser -p mypass
```

To export the boot device cert with index 2 to a remote HTTPS share:

```
racadm httpsbootcert export -i 2 -f httpsboot_cert.crt -l https://192.168.10.24/share -u myuser -p mypass
```

To export the boot device cert with index 3 to local share using local racadm:

```
racadm httpsbootcert export -f httpsboot_cert.pem
```

To export the boot device cert with index 4 to a local share using remote racadm:

```
racadm -r 10.94.161.119 -u root -p calvin httpsbootcert export -f httpsboot_cert.txt
```

NOTE: These commands do not support setting the proxy parameters if the share location is HTTP/HTTPS. To perform the operation with HTTP or HTTPS via a proxy, the proxy parameters must be first configured using the lifecyclecontroller.lcattributes group. Once these proxy parameters are configured, they become the part of default configuration. The proxy attributes should be cleared to end use of the HTTP/HTTPS proxy. The valid lifecyclecontroller.lcattributes HTTP/HTTPS proxy parameters are: UserProxyUserName, UserProxyPassword, UserProxyServer, UserProxyPort, UserProxyType. To view the list of proxy attributes, use racadm get lifecycleController.lcAttributes.

To delete the boot device cert with index 1:

```
racadm httpsbootcert delete -i 1
```

To delete the boot device cert with index 2:

```
racadm httpsbootcert delete -i 2
```