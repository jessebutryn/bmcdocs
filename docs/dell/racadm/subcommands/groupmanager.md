# groupmanager

## Description

Allows you to:

- Delete the group from the group manager.
- Remove the iDRAC from group by itself by using admin privileges.
- Join the group using administrator privileges.

NOTE: This subcommand is supported only on iDRAC9.

## Synopsis

- To delete the group from the group manager.

```
groupmanager delete –g <groupname>
```

- To remove the iDRAC from group by itself by using administrator privileges.

```
groupmanager removeself –g <groupname>
```

- To join the group using administrator privileges.

```
groupmanager joingroup -g <groupname> -uid <uuid> -pcode <grouppasscode>
```

## Input

- `-g` — Specifies the name of the iDRAC member group
- `-uid` — Specifies the group user id
- `-pcode` — Specifies the group passcode

## Output/Example

To delete the group from the groupmanager:

```
racadm groupmanager delete –g <groupname>
```

To remove the iDRAC from the group by itself:

```
racadm groupmanager removeself –g <groupname>
```

To join server to the local iDRAC group:

```
racadm groupmanager joingroup -g <mygrpxyz> -uid <uid1234> -pcode <12345>
```