# BootstrappingAccount

Manages bootstrapping accounts for Redfish Host Interface. Creates random accounts or deletes existing bootstrapping accounts.

## Syntax

```
sum [-I Redfish_HI -u <username> -p <password>] -c BootStrappingAccount --action <action> [--user_name <username>]
```

## Actions

- **1**: Create a new bootstrapping account
- **2**: Delete an existing bootstrapping account (requires `--user_name`)
- **3**: Check existing bootstrapping accounts

## Options

- `--action <action>`: Required. Action to perform (1=create, 2=delete, 3=check)
- `--user_name <username>`: Username of account to delete (required for action 2)

## Examples

### In-Band
```bash
# Create a new bootstrapping account
[SUM_HOME]# ./sum -c BootStrappingAccount --action 1

# Create account with Redfish Host Interface
[SUM_HOME]# ./sum -I Redfish_HI -u ADMIN -p ADMIN -c BootStrappingAccount --action 1

# Check existing accounts
[SUM_HOME]# ./sum -I Redfish_HI -u ADMIN -p ADMIN -c BootStrappingAccount --action 3

# Delete a specific account
[SUM_HOME]# ./sum -I Redfish_HI -u ADMIN -p ADMIN -c BootStrappingAccount --action 2 --user_name 'xxxxxxxxxxxxxxx'
```

## Notes

- Administrator privileges are needed to delete a bootstrapping account
- Delete/check functions only available with `-I Redfish_HI`
- System reboot or BMC reset automatically deletes bootstrapping accounts
- Only local in-band usage is supported
- Maximum of two bootstrapping accounts supported
- Username must be in single quotes on Linux or double quotes on Windows when deleting
- When using `-I Redfish_HI` without `-u` and `-p` and no existing bootstrapping account, SUM creates one automatically
