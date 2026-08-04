# BootStrappingAccount

Gets a random account for the Redfish Host Interface or deletes an existing bootstrapping account. Only local in-band usage is supported.

## Syntax

### In-Band
```
saa [-I Redfish_HI -u <username> -p <password>] -c BootStrappingAccount --action <CreateAccount | DeleteAccount | CheckAccount> [--user_name <username>]
```

## Options

- `--action <action>`: Required. Sets action to `1` = CreateAccount, `2` = DeleteAccount, `3` = CheckAccount
- `--user_name <user name>`: Deletes a bootstrapping account with the given user name (used with `--action DeleteAccount`)

## Examples

### In-Band
```bash
[SAA_HOME]# ./saa -c BootStrappingAccount --action 1
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p ADMIN -c BootStrappingAccount --action 1
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p ADMIN -c BootStrappingAccount --action 3
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p ADMIN -c BootStrappingAccount --action 2 --user_name 'xxxxxxxxxxxxxxx'
```

## Notes

- Administrator privileges are needed to delete a bootstrapping account.
- Deleting or checking an account is only available when using `-I Redfish_HI`.
- A system reboot or BMC reset automatically deletes a bootstrapping account.
- Only local in-band usage is supported.
- Only two bootstrapping accounts are supported.
- To delete a bootstrapping account, the user name must be enclosed in single quotation marks on Linux systems or double quotation marks on Windows systems.
