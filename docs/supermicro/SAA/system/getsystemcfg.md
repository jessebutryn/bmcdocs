# GetSystemCfg

Gets the current system settings from the managed system and saves them to the `SystemCfg.xml` file. System settings include BIOS settings and BMC settings.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c GetSystemCfg --file <SystemCfg.xml> [--overwrite] [[--download] [--file_id]]
```

### In-Band
```
saa -c GetSystemCfg --file <SystemCfg.xml> [--overwrite] [[--download] [--file_id]]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c GetSystemCfg --file <SystemCfg.xml> [--overwrite] [[--download] [--file_id]]
```

## Options

- `--file <file name>`: Saves the configuration to a file.
- `--current_password <current password>`: Checks the current BIOS Administrator password.
- `--download`: Downloads the current Blade system configuration file accessible for profile update from the CMM.
- `--file_id <file ID>`: Downloads the existing Blade system profile from the CMM with the specific file ID.
- `--overwrite`: Overwrites the output file.
- `--dev_id <Device ID>`: Assigns Blade index and node ID. Blade index: `[A1-A14]` or `[B1-B14]`; Node ID: `[1-4]`; format example: `A1_1`.
- `--cur_pw_file <Current password file>`: The specified file path to read the BIOS Administrator password.
- `--action <action>`: Sets the action for each XML table. Acceptable options: `None` or `Change`.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetSystemCfg --file SystemCfg.xml --overwrite

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetSystemCfg --file SystemCfg.xml --download --dev_id A1_1

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c GetSystemCfg --file SystemCfg_Cache.xml --download --file_id 2
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c GetSystemCfg --file SystemCfg.xml --overwrite
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

If the Status field of a managed system (e.g. 192.168.34.56) shows SUCCESS, its current settings are stored in its output file, e.g. `SystemCfg.xml.192.168.34.56`. The `--overwrite` option forces an existing file of the same name to be overwritten.

## Notes

- The tables/elements from the managed systems might not be identical; only tables/elements supported by the managed system are accessed.
- A configuration file in XML can be downloaded from the CMM via the `--download` option. This feature is only supported by the 64MB CMM AST2400.
