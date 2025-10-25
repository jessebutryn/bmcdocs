# update

## Description

Allows you to update the firmware of devices on the server. The supported firmware image file types are:

- .exe — Windows-based Dell Update Package (DUP)
- .d9
- .pm
- .sc

The supported catalog files are:

- .xml
- xml.gzip

## Synopsis

For single file or DUP update:

```
racadm update -f <updatefile>
racadm update -f <updatefile> -l <location> -u <username for CIFS share> -p <password for CIFS share>
racadm update -f <updatefile> -l <location>
```

For Repository updates:

```
racadm update -f <catalog file> -t <Repository type> -l <location> -u <username for CIFS share> -p <password for CIFS share> [-a <restart>] [--verifycatalog]
racadm update -f <catalog file> -t <Repository type> -e <FTP server with the path to the catalog file> [-a <restart>] [--verifycatalog]
racadm update -f <catalog file> -t <Repository type> -e <FTP server with the path to the catalog file> [-a <restart>] -ph <proxy ip> -pu <proxy user> -pp <proxy pass> -po <proxy port> -pt <proxy type>
racadm update viewreport
```

## Input

For single file or DUP update:

- `-f: <updatefile>` — Update filename (Windows DUP, .d9,.pm, .sc) only.
- `-u: <username for CIFS share>` — Specifies username of the remote share that stores the update file. Specify username in a domain as domain/username.
- `-p: <password for CIFS share>` — Specifies password of the remote share that stores the update file.
- `-l: <location>` — Specifies network share location that stores the update file.
- `--reboot` — Performs a graceful system reboot after the firmware update.

For Repository update:

- `-f: <updatefile>` — Update filename.
- `-u: <username for CIFS share>` — Username of the remote share that stores the update file. Specify username in a domain as domain/username.
- `-p: <password for CIFS share>` — Specifies password of the remote share that stores the update file.
- `-l: <location>` — Specifies network share location (CIFS/NFS/HTTP/HTTPS/FTP/TFTP), that stores the update file.
- `-a: <restart>` — This option indicates if the server should be restarted after the update from repository operation completes. Must be one of the below:
    - TRUE: restart after update completes
    - FALSE: do not restart after update completes
- `-t: <Repository type>` — Specifies the type of repository being used for the update. Must be one of the below:
    - FTP: Repository is FTP
    - TFTP: Repository is TFTP
    - HTTP: Repository is HTTP
    - HTTPS: Repository is HTTPS
    - CIFS: Repository is CIFS
    - NFS: Repository is NFS
- `-e: <FTP server with the path to the catalog file>` — Specifies the Server path for the FTP, TFTP, HTTP, and HTTPS.
- `-ph: <proxy ip>` — Specifies the IP address of the proxy server.
- `-pu: <proxy user>` — Specifies the user name for proxy credentials.
- `-pp: <proxy pass>` — Specifies the password for proxy credentials.
- `-po: <proxy port>` — Specifies the port for proxy server.
- `-pt: <proxy type>` — Specifies the proxy type. Must be one of the below:
    - HTTP: Proxy is HTTP
    - SOCKS4: Proxy is SOCKS4

## Output/Example

Upload the update file from a remote FTP share.

```
racadm update -f <updatefile> -u admin -p mypass -l ftp://1.2.3.4/share
```

Upload the update file from a remote FTP share and perform a graceful system reboot after update.

```
racadm update -f <updatefile> -u admin -p mypass -l ftp://1.2.3.4/share --reboot
```

Upload the update file from a remote CIFS share.

```
racadm update -f <updatefile> -u admin -p mypass -l //1.2.3.4/share
```

Upload the update file from a remote CIFS share and under a user domain "dom".

```
racadm update -f <updatefile> -u dom/admin -p mypass -l //1.2.3.4/share
```

Upload the update file from a remote NFS share.

```
racadm update -f <updatefile> -l 1.2.3.4:/share
```

Upload the update file from a remote HTTP share.

```
racadm update -f <updatefile> -u admin -p mypass -l http://1.2.3.4/share
```

Upload the update file from a remote HTTPS share.

```
racadm update -f <updatefile> -u admin -p mypass -l https://1.2.3.4/share
```

Upload the update file from the local file system using Local RACADM.

```
racadm update -f <updatefile>
```

Upload the Update file from a remote CIFS share and perform a graceful system reboot after update.

```
racadm update -f <updatefile> -u admin -p mypass -l //1.2.3.4/share --reboot
```

Upload the Update file from a remote NFS share and perform a graceful system reboot after update.

```
racadm update -f <updatefile> -l 1.2.3.4:/share --reboot
```

Upload the update file from a remote HTTP share and perform a graceful system reboot after update.

```
racadm update -f <updatefile> -u admin -p mypass -l http://1.2.3.4/share --reboot
```

Upload the Update file from the local file system using local racadm and perform a graceful system reboot after update.

```
racadm update -f <updatefile> --reboot
```

Perform update from an FTP repository and apply the updates, reboot the server.

```
racadm update -f Catalog.xml -l //192.168.11.10/Repo -u test -p passwd -a TRUE -t CIFS
```

Generate a comparison report using about the available updates in the repository.

```
racadm update -f Catalog.xml -l 192.168.11.10:/Repo -t NFS -a FALSE --verifycatalog
```

Perform update from an FTP repository and reboot the server to apply the updates.

```
racadm update -f Catalog.xml -e 192.168.11.10/Repo/MyCatalog -a TRUE -t FTP
```

Perform update from an FTP repository with authentication and reboot the server to apply the updates.

```
racadm update -f Catalog.xml -e 192.168.11.10/Repo/MyCatalog -u user -p mypass -a TRUE -t FTP
```

Perform update from a HTTP repository and restart the server to apply the updates.

```
racadm update -f Catalog.xml -e 192.168.11.10/Repo/MyCatalog -a TRUE -t HTTP
```

Perform update from a TFTP repository and restart the server to apply the updates.

```
racadm update -f Catalog.xml -e 192.168.11.10/Repo/MyCatalog -a TRUE -t TFTP
```

Perform update from an FTP repository through a proxy server.

```
racadm update -f Catalog.xml -e 192.168.11.10/Repo/MyCatalog -a TRUE -ph 145.140.12.56 -pu prxyuser -pp prxypass -po 80 -pt http -t FTP
```

Perform update from downloads.dell.com.

```
racadm update -f Catalog.xml.gz -e ftp.dell.com/Catalog -a TRUE -t FTP
```

View the comparison report generated when --verifycatalog is used.

```
racadm update viewreport
```