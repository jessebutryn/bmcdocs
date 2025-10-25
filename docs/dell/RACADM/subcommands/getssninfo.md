# getssninfo

## Description

Displays a list of users that are connected to iDRAC. The following information is displayed:

- Session ID
- Username
- IP address (if applicable)
- Session type
- Login date and time in MM/DD/YYYY HH:MM:SS format

NOTE: Based on the Session ID (SSNID) or the user name (User), the iDRAC administrator can close the respective sessions or all the sessions using the closessn subcommand. For more information, see closessn.

## Synopsis

```
racadm getssninfo [-u <username>] [-A]
```

## Input

- `-u` — displays only sessions associated with a specific user.
- `-A` — does not display headers or labels.

## Output/Example

```
racadm getssninfo
```

```
SSNID Type User IP Address Login Date/Time
58999 SSH  root 192.168.0.100 4/07/2016 12:00:34
```

Display the details of sessions without header

```
racadm getssninfo -A
```

```
"43584" "SSH" "root" "192.168.0.10" "04/07/2016 12:00:34"
```