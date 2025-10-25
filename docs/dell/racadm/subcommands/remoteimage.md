# remoteimage

## Description

Connects, disconnects, or deploys a media file on a remote server.

To run this subcommand, you must log in with virtual media privilege for iDRAC.

## Synopsis

```
racadm remoteimage -d
racadm remoteimage -s
racadm remoteimage -c [-u <username> -p <password> -l <image_path>]
```

## Input

- `-c` — Connect the image.
- `-d` — Disconnect image.
- `-u` — User name to access shared folder.
- `-p` — Password to access shared folder.
- `-l` — Image location on the network share; use single quotation marks around the location.
- `-s` — Display current status.

NOTE: Use a forward slash (/) when providing the image location. If backward slash (\) is used, override the backward slash for the command to run successfully.

For example:

```
racadm remoteimage -c -u user -p xxx -l /\/\192.168.0.2/\CommonShare/ \diskette
```

NOTE: The following options only apply to connect and deploy actions

- `-u` — Username.
  User name to access the network share. For domain users, you can use the following formats:
  - domain/user
  - domain\user
  - user@domain
- `-p` — Password to access the network share.

## Output/Example

Disable Remote File Sharing.

```
racadm remoteimage -d
```

```
Disable Remote File Started. Please check status using -s option to
know Remote File Share is ENABLED or DISABLED.
```

Check Remote File Share status.

```
racadm remoteimage -s
```

```
Remote File Share is Enabled
UserName
Password
ShareName //192.168.0/xxxx/dtk_3.3_73_Linux.iso
```

Deploy a remote image on iDRAC CIFS Share.

```
racadm remoteimage -c -u admin -p xxx -l //192.168.0.32/dev/OM840.iso
```

Deploy a remote image on iDRAC NFS Share.

```
racadm remoteimage -c -u root -p password -l '192.168.1.113:/opt/nfs/ OM840.iso
```

Deploy a remote image on iDRAC HTTP Share.

```
racadm remoteimage -c -u "user" -p "xxx" -l http://shrloc/foo.iso
```

Deploy a remote image on iDRAC HTTPS Share.

```
racadm remoteimage -c -u "user" -p "xxx" -l https://shrloc/foo.iso
```

NOTE: -p and -u options are not mandatory in case of HTTP/HTTPS based remoteimage commands.