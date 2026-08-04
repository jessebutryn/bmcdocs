# RedfishApi

Invokes any Redfish API and displays the response on screen.

## Syntax

### Single System OOB
```
saa -i <IP or host name> -u <username> -p <password> -c RedfishApi --api <api path> [-v] [--request <http method>] [--file <file name> [--overwrite]] [--data <request body>] [--retry <number>]
```

### Single System In-Band
```
saa -I Redfish_HI -u <username> -p <password> -c RedfishApi --api <api path> [-v] [--request <http method>] [--file <file name> [--overwrite]] [--data <request body>] [--retry <number>]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c RedfishApi --api <api path> [-v] [--request <http method>] [--file <file name> [--overwrite]] [--data <request body>] [--retry <number>] [--individually]
```

## Options

- `--api <api path>`: Redfish API path.
- `-v`: Displays the response header (verbose output).
- `--request <HTTP method>`: HTTP method (GET, POST, or PATCH). The default setting is GET.
- `--file <file name>`: Outputs the response to a file instead of printing on screen.
- `--overwrite`: Overwrites the output file.
- `--data <request body>`: The request body for the POST and PATCH methods. Can be supplied directly as a string (special characters must be escaped), or stored in a text file and referenced by prepending an at character (`@`) to the file name, e.g. `--data @body.txt`.
- `--retry <Number>`: Number of retry times. The default value is 3.
- `--individually`: Reads the request body from the file individually. Only supported for multiple systems OOB usage.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c RedfishApi --api /redfish/v1/TaskService

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c RedfishApi --request PATCH --api /redfish/v1/TaskService --data "{\"ServiceEnabled\":true}"

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c RedfishApi --request PATCH --api /redfish/v1/TaskService -v --retry 1 --data @body.txt --file response.txt --overwrite
```

### In-Band
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c RedfishApi --api /redfish/v1/TaskService

[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c RedfishApi --request PATCH --api /redfish/v1/TaskService --data "{\"ServiceEnabled\":true}"

[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p PASSWORD -c RedfishApi --request PATCH --api /redfish/v1/TaskService -v --retry 1 --data @body.txt --file response.txt --overwrite
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c RedfishApi --request PATCH --api /redfish/v1/TaskService -v --retry 1 --data @body.txt --file response.txt --overwrite --individually
```

## Notes

- To invoke a Redfish API against 192.168.34.56 and 192.168.34.57 with different request bodies, provide two files, `body.txt.192.168.34.56` and `body.txt.192.168.34.57`, then specify `--data @body.txt`. With `--individually`, SAA looks for `body.txt.192.168.34.56` and `body.txt.192.168.34.57` as the request bodies sent to each respective system.
