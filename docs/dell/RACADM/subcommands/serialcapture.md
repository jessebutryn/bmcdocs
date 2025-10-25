# serialcapture

## Description

The serialcapture subcommand is used to export and clear serial data captured from the system.

To run this subcommand, you must have the following privileges:

## Synopsis

To clear serial data.

```
racadm serialcapture clear
```

To export serial data.

```
racadm serialcapture export -u <shareuser> -p <sharepassword> -l <NFS/ CIFS/HTTP/HTTPS share> -f <FileName>
```

## Input

- `-f` — Filename of the exported serial data.
- `-u` — Username of the remote share to where the file must be exported. The username must be specified as domain/username.
- `-p` — Password for the remote share to where the file must be exported.
- `-l` — Network share location to where the serial data captured must be exported. For more information on NFS or CIFS or HTTP or HTTPS share, see section on Usage examples.

## Output/Example

To clear serial data buffer.

```
racadm serialcapture clear
```

To export serial data to CIFS share.

```
racadm serialcapture export -u cifsuser -p cifspassword -l //1.2.3.4/ cifsshare -f datafile
```

To export serial data to NFS share.

```
racadm serialcapture export -u nfssuser -p nfspassword -l 1.2.3.4:/ nfsshare -f datafile
```

To export serial data to HTTP share.

```
racadm serialcapture export -u httpuser -p httppassword -l http:/1.2.3.4/ httpshare -f datafile
```

To export serial data to HTTPS share.

```
racadm serialcapture export -u httpsuser -p httpspassword -l https:/ 1.2.3.4/cifsshare -f datafile
```