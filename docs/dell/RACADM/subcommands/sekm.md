# sekm

## Description

The sekm subcommand is used to enable and disable sekm support for a server, rekey sekm-supported devices on a server, and test the SSL connection to a given sekm server.

To run this subcommand, you must have the following privileges:

- Enable — server control and configure iDRAC privileges
- Disable — server control and configure iDRAC privileges
- Rekey — server control and configure iDRAC privileges
- Testserverconnection — server control and configure iDRAC privileges
- Getstatus — login privileges

NOTE: To run enable, disable, and testserverconnection commands, the target server must have sekm license.

## Synopsis

To get sekm status.

```
racadm sekm getstatus
```

To enable sekm feature.

```
racadm sekm enable
```

NOTE: When you execute racadm sekm enable, a job ID is returned, query this job id to see the status of sekm. If the query reports failure, check the job ID config results or LC logs to find the reason for failure.

To disable sekm feature.

```
racadm sekm disable
```

To request iDRAC to rekey all the devices.

```
racadm sekm rekey <IDRAC FQDD>
```

To test primary sekm server connection.

```
racadm sekm testserverconnection -p -i <index of the sekm server>
```

To test the secondary sekm server connection.

```
racadm sekm testserverconnection -s -i <index of the sekm server>
```

## Input

- `-i` — Index of the sekm server to test
- `-p` — Indicates primary sekm server
- `-s` — Indicates secondary sekm server

## Output/Example

To get sekm status.

```
racadm sekm getstatus
```

To enable sekm feature.

```
racadm sekm enable
```

To disable sekm feature.

```
racadm sekm disable
```

To request iDRAC to rekey all the devices.

```
racadm sekm rekey iDRAC.Embedded.1
```

To test primary sekm server connection.

```
racadm sekm testserverconnection -p -i 1
```

To test the secondary sekm server connection.

```
racadm sekm testserverconnection -s -i 1
```

NOTE: Only one primary server is supported. Option -i should be 1.

NOTE: For sekm getstatus, the returned values and their meaning are as follows:

- Disabled — sekm functionality has been disabled on iDRAC and no sekm functions are available.
- Enabled — sekm functionality has been enabled on iDRAC and all sekm functions are available.
- Failed — iDRAC is unable to communicate with the sekm server.
- Unverified Changes Exist — Changes have been made to the sekm configuration but not yet enabled using the racadm sekm enable command.