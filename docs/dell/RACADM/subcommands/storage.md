# storage

## Description

Displays storage information for the system, including controllers, physical disks, virtual disks, and enclosures.

## Synopsis

```bash
racadm storage get controllers
racadm storage get pdisks
racadm storage get vdisks
racadm storage get enclosures
racadm storage get <component> -o <object>
```

## Common Commands

- Get all controllers: `racadm storage get controllers`
- Get physical disks: `racadm storage get pdisks`
- Get virtual disks: `racadm storage get vdisks`
- Get enclosures: `racadm storage get enclosures`
- Get specific object: `racadm storage get <FQDD> -o <object>`

## Examples

- Display all storage controllers: `racadm storage get controllers`
- Display physical disks on a controller: `racadm storage get pdisks -c <controller_FQDD>`
- Display virtual disks: `racadm storage get vdisks`

For detailed storage configuration and management, see the full RACADM documentation.