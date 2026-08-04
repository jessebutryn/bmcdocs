# RemoteExec

Sends files and executes shell commands on a remote system. Manages remote systems with in-band usage.

## Syntax

### Remote In-Band
```
saa -I Remote_INB --oi <OS IP address> --ou <OS username> [--op <OS password> | --os_key <OS private key> --os_key_pw <OS private key password>] -c RemoteExec --remote_cmd <shell command> [--file <file name>]
```

### Multiple Systems Remote In-Band
```
saa -I Remote_INB -l <system list file> -c RemoteExec --remote_cmd <shell command> [--file <file name>]
```

## Options

- `--remote_cmd <Remote command>`: Enters the commands to be executed on remote Linux systems.
- `--file <file name>`: Transfers the file(s) to a remote system.

## Examples

### Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB --oi 192.168.34.57 --ou root --op 111111 -c RemoteExec --remote_cmd "ls ~/supermicro/saa_remote_inband/ -l | grep test.sh" --file test.sh
```

### Multiple Systems Remote In-Band
```bash
[SAA_HOME]# ./saa -I Remote_INB -l Slist.txt -c RemoteExec --remote_cmd "ls ~/supermicro/saa_remote_inband/ -l | grep test.sh" --file test.sh
```

`SList.txt` for multiple systems remote in-band usage takes the form:
```
192.168.34.56 root 111111
192.168.34.57 root 111111
```

## Notes

- If the execution "Status" field of the managed system shows SUCCESS, the console output of the managed system will be shown in the "Execution Message" section of the managed system in the created log file.
- The stderr in the remote system will be redirected to stdout.
- For use with tested third-party tools, refer to the "Using SAA to Run 3rd-Party Tools" appendix.
