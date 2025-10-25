# eventfilters

## Description

Displays the list of event filter settings.

To use this subcommand with the set and test option, you must have the Administrator privilege.

## Synopsis

```
racadm eventfilters get -c <alert category>
racadm eventfilters set -c <alert category> -a <action> -n <notifications>
racadm eventfilters set -c <alert category> -a <action> -r <recurrence>
racadm eventfilters test -i <Message ID to test>
```

## Input

- `-c` — Alert category of the specific event filter
- `-a` — The action that must be invoked when the event occurs. Valid values are none, powercycle, poweroff, or systemreset
- `-n` — The notification is sent when the event occurs. Valid values are all, snmp, ipmi, ws-events, redfish-events, oslog, remotesyslog, email, or none. You can append multiple notifications that are separated by a comma. You cannot enter the values all or none with other notifications.
- `-r` — Event generation interval. This option is applicable only to the temperature statistics subcategory tmps. You can use this option as a stand-alone or with -n and -a. The valid values are 0–365. 0 disables the event generation.
- `-i` — Message ID for which the simulation is needed

## Output/Example

Display all available event filter configurations.

```
racadm eventfilters get -c idrac.alert.all
```

Display eventfilter configurations for a specific category. For example, audit.

```
racadm eventfilters get -c idrac.alert.audit
```

Display eventfilter configurations for a specific subcategory. For example, licensing under the audit category.

```
racadm eventfilters get -c idrac.alert.audit.lic
```

Display eventfilter configurations for a specific severity. For example, warning under the audit category.

```
racadm eventfilters get -c idrac.alert.audit.warning
```

Display eventfilter configurations for a specific severity and subcategory. For example, a severity of warning in the subcategory licensing under audit category.

```
racadm eventfilters get -c idrac.alert.audit.lic.warning
```

Clear all available alert settings.

```
racadm eventfilters set -c idrac.alert.all -a none -n none
```

Configure using severity as a parameter. For example, all informational events in storage category are assigned power off as action, and email and SNMP as notifications.

```
racadm eventfilters set -c idrac.alert.storage.info -a poweroff -n email,snmp
```

Configure using subcategory as a parameter. For example, all configurations under the licensing subcategory in the audit category are assigned power off as action and all notifications are enabled.

```
racadm eventfilters set -c idrac.alert.audit.lic -a poweroff -n all
```

Configure using subcategory and severity as parameters. For example, all information events under the licensing subcategory in the audit category are assigned power off as action and all notifications are disabled.

```
racadm eventfilters set -c idrac.alert.audit.lic.info -a poweroff -n none
```

Configure the event generation interval for temperature statistics.

```
racadm eventfilters set -c idrac.alert.system.tmps.warning -r 10
```

Configure the event generation interval and notifications for temperature statistics.

```
racadm eventfilters set -c idrac.alert.system.tmps -r 5 -a none -n snmp
```

Send a test alert for the fan event.

```
racadm eventfilters test -i FAN0001
```