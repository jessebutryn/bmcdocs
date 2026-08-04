# ProfileManage

Manages the CMM and system configuration profile information stored on the CMM (get, edit, and delete). Profile update is only supported on Blade systems with a 64MB CMM AST2400.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c ProfileManage --action <action> [--file <filename> [--overwrite]] [--file_id] [--profile_name] [--profile_description] [--schedule_update_time] [--showall]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c ProfileManage --action <action> [--file <filename>]
```

## Actions

- **Get**: Gets the profile list.
- **Edit**: Edits profile information.
- **Delete**: Deletes a profile.

## Options

- `--action <action>`: Sets action to `Get`, `Edit`, or `Delete`.
- `--file <file name>`: Saves the profile list to a file. Prints the profile list on the screen if the file-saving function is not available (optional).
- `--file_id <file ID>`: Gets and edits profile information, or deletes the profile on CMM, with the specific file ID (optional).
- `--profile_name <profile name>`: Edits the profile name of the specified profile on CMM with the specific file ID (optional).
- `--profile_description <profile description>`: Edits the profile description of the specified profile on CMM with the specific file ID (optional).
- `--schedule_update_time <schedule update time>`: Edits the scheduled update time of the specified profile on CMM with the specific file ID. Format: `[YYYY-MM-DD_HH:MM]` (optional).
- `--overwrite`: Overwrites the output file.
- `--showall`: Gets the profile association information between the specified profile and the selected Blade systems with a specific profile ID.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ProfileManage --action Get

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ProfileManage --action Edit --file_id 2 --profile_description 'For_Blade_A2'

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ProfileManage --action Delete --file_id 2
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ProfileManage --action Get --file Profile.xml
```

## Output

### Get (with --showall)
```
Managed system...........192.168.34.56
Profile ID: 1
==============
Profile Type: Cmm
Profile Name: cmmcfg.xml
Profile Description: For_CMM
Schedule Update Time: 2021-09-07_14:28

Profile ID: 2
==============
Profile Type: System
Profile Name: systemcfg.xml
Profile Description: For_Blade_A1
Schedule Update Time: 2021-09-07_14:28
```

### Get (multiple systems, with profile association)
```
Profile ID: 2
==============
Profile Type: System
Profile Name: systemcfg_TEST.xml
Profile Description: TEST
Schedule Update Time: 2022-09-20_15:44
Profile Association:
 Blade: B6 Node: 1 Status: Waiting for scheduling update
 Blade: B6 Node: 2 Status: Waiting for receiving profile
 Blade: B6 Node: 3 Status: Waiting for receiving profile
 Blade: B6 Node: 4 Status: Waiting for receiving profile
 Blade: B10 Node: 1 Status: Waiting for scheduling update
```

### Edit
```
Profile ID "2" is edited.
Profile ID: 2
==============
Profile Type: System
Profile Name: systemcfg.xml
Profile Description: For_Blade_A2
Schedule Update Time: 2021-09-07_14:28
```

### Delete
```
Profile ID "2" is deleted.
```

## Notes

- There is a space limit on profiles. Once the space is full, use `ProfileManage` to delete unnecessary profiles before uploading new ones.
- Each profile name on CMM is unique — different profiles with the same profile name cannot exist on the CMM at the same time.
- SAA supports two update actions for applying a profile: `Apply` and `Deploy` (used with `ChangeCmmCfg`/`ChangeSystemCfg --update`). `Apply` updates existing Blade systems (immediately if the scheduled time has passed, or at the scheduled time). `Deploy` updates Blade systems that have been replaced or newly plugged in, in addition to existing systems. One Blade system only accepts one update rule; a new rule always replaces the older one.
- If the Status field for a managed system shows SUCCESS, the profile information is shown in the Execution Message section of the created log file.
