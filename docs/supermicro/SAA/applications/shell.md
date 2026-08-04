# Shell

Enters Shell Mode, in which multiple commands can be run on a managed server without exiting the SAA tool. OOB only.

## Syntax

### Single System OOB
```
saa -i <IP or host name> -u <username> -p <password> -c Shell
```

## Options

None.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c Shell
```

## Output

```
Index | IP Board DC Room Row Rack Num Type | BMC
----- | ---------------- ----- ---- ---- ---- ---- ---- ---- | -------
 1 | 169.254.3.254 |
 2 | 10.184.3.166 |
 3 | 10.184.3.170 |
 4 | 10.184.3.185 |
4 IPMI device(s) found.
Managed hosts loaded.Found hosts loaded.Done
Press Ctrl+D or "exit" to exit
Press "?" or "help" for help
Press UP and DOWN key for command history
ADMIN@192.168.34.56 X13SEI-TF/-F (S0/G0 Working,83w,01.01.05) 15:44
X13_RoT2.0_ATEN_AST2600_1_1>
```

## Notes

- In Shell Mode, you can execute multiple commands on the managed server, using command history (Up/Down keys) and inline help (`?` or `help`).
- Press `Ctrl+D` or type `exit` to leave Shell Mode.
- The related information shown in the prompt (username, IP address, motherboard, ACPI status, power consumption, firmware version, current time, firmware type) can be configured with the `Prompt` command.
