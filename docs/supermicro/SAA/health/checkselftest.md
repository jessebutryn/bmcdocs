# CheckSelfTest

Shows the basic health status of the BMC system.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c CheckSelfTest
```

### In-Band
```
saa -c CheckSelfTest
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c CheckSelfTest
```

## Options

None

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CheckSelfTest
```

### In-Band
```bash
[SAA_HOME]# ./saa -c CheckSelfTest
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c CheckSelfTest
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

If the execution "Status" field of the managed system shows SUCCESS, the console output of the managed system is shown in the "Execution Message" section of the created log file.

## Output

The self-test result is one of several possible status lines, depending on BMC health, for example:

```
Self Test is passed
```

```
Self Test function not implemented in this controller
```

```
[Controller operational firmware corrupted]
Corrupted or inaccessible data or device
```

```
[Controller update boot block corrupted]
Corrupted or inaccessible data or device
```

```
[Internal Use Area corrupted]
Corrupted or inaccessible data or device
```

```
[SDR repository empty]
Corrupted or inaccessible data or device
```

```
[IPMB signal lines do not respond]
```

```
[FRU device not accessible]
Corrupted or inaccessible data or device
```

```
[SDR repository not accessible]
Corrupted or inaccessible data or device
```

```
[SEL device not accessible]
Corrupted or inaccessible data or device
```

```
Fatal hardware error
```

```
N/A
```

```
Device specific, CCh
```
