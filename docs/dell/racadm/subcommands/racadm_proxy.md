# racadm proxy

## Description

On the PowerEdge FX2/FX2s systems, you can manage the compute sleds and CMC using the iDRAC's RACADM Proxy feature that redirects commands from iDRAC to CMC. You can return the CMC response to local or remote RACADM to access the CMC configuration and reporting features without placing the CMC on the management network.

## Synopsis

Local RACADM proxy usage:

```
racadm <CMC racadm subcommand> --proxy
```

Remote RACADM proxy usage:

```
racadm <CMC racadm subcommand> -u <username> -p <password> -r <idrac-ip connected to cmc> --proxy
```

## Input

- `-u` — Specifies the user name of the remote share that stores the catalog file.
- `-p` — Specifies the password of the remote share that stores the catalog file.
- `-r` — Specifies the iDRAC IP address connected to CMC.
- `--proxy` — Must be entered at the end of the command.

## Output/Example

Local RACADM proxy.

```
racadm getractime --proxy
```

Remote RACADM proxy.

```
racadm getractime -u root -p xxx -r 192.168.0.1 --proxy
```