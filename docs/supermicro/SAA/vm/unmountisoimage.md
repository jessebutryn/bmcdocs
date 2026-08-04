# UnmountIsoImage

Removes an ISO image as virtual media from the managed system. This command is only supported on platforms that support a single virtual media device.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c UnmountIsoImage [--redfish]
```

### In-Band
```
saa -u <username> -p <password> -c UnmountIsoImage
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c UnmountIsoImage
```

## Options

- `--redfish` (Optional): Enables support for pure Redfish.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c UnmountIsoImage
```

### In-Band
```bash
[SAA_HOME]# ./saa -c UnmountIsoImage
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c UnmountIsoImage
```

## Output

If the execution "Status" field for a managed system is SUCCESS, the mounted virtual media will be removed from the managed system.

## Notes

- This command is only supported on platforms that support a single virtual media device only.
- Special characters for ID and password: `^` (caret).
- Special characters for shared host: `-` (dash) or `.` (period).
- Special character for HTTP and SAMBA protocols in an IPv6-format URL shared host: `:` (colon). The shared host for the HTTP protocol in IPv6 format must be enclosed with square brackets `[ ]`.
- Special characters for path to image: `@^-_./\` (`/` and `\` can only be used in a path).
- Special characters like backslashes `\` and slashes `/` should only be used once; repeated use (e.g., `//`, `\\`, `/\` and `\/`) is not allowed.
- Special character `^` (caret) is not available for use in older versions of BMC firmware.
- The port number may not be supported in older versions of BMC firmware.
- An IPv6 link-local address starting with `fe80` is not allowed.
