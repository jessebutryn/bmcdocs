# CpuOnDemand

Supports Intel® On Demand Capabilities (IOD) on Intel® Xeon SPR (Sapphire Rapids) and later CPUs, activating additional features during the lifetime of the selected Xeon CPUs. IOD requires interaction with Supermicro tools and Intel and involves four actions used together: `GetHwInfo`, `GetOnDemandState`, `SetLicenseActivateCode`, and `EnablePPIN`.

## CpuOnDemand Flow

1. Ensure the CPU is compatible with IOD and run `--action GetHwInfo` to get hardware information, e.g. PPIN and CPU socket index.
2. Provide the PPIN and system asset information to Supermicro to obtain a LAC+ file.
3. Apply the LAC+ file and run `--action SetLicenseActivateCode` to provision the CPU.
4. Run `--action GetOnDemandState` to get a state report file.
5. Send the state report file back to Supermicro, which forwards it to Intel.

## Options

- `--action <action>`: Sets the action:
    - `1` = GetHwInfo
    - `2` = GetOnDemandState
    - `3` = SetLicenseActivateCode
    - `4` = EnablePPIN
- `-v`: Prints extra info of CAP and registers, used with action 2 = GetOnDemandState.
- `--cpu_id <CPU ID>`: CPU ID to indicate the CPU socket.
- `--hw_id <Hardware ID>`: Hardware ID to indicate the PPIN of the CPU socket.
- `--hw_id_file <Hardware ID file>`: Hardware ID file with the format `BMC MAC;CPU ID;PPIN`.
- `--lac_file <LAC+ map file>`: License file in the format `PPIN;LAC+(s)`, used in action 3 = SetLicenseActivateCode.
- `--cfg_file <SDSi-agent config file>`: SDSi-agent config file, only useful in action 2 = GetOnDemandState when specifying `-v`.
- `--skip_gap <Skip gap(s)>`: Skips the gap of LAC revision ID and continues provisioning.
- `--squash <Squash into one file>`: Squashes the state reports into one file in the format `PPIN;State Report`.
- `--plain_text <Output state as plain text>`: Prints the on-demand state as plain text.
- `--file <file name>`: Saves to file in action 1 = GetHwInfo and action 2 = GetOnDemandState, or provides the license file in action 3 = SetLicenseActivateCode.
- `--reboot`: (Optional) Forces the managed system to reboot or power up after the operation.
- `--post_complete`: (Optional) Waits for the managed system POST to complete after rebooting.
- `--overwrite`: (Optional) Overwrites the hardware ID or on-demand state report file.

## Examples

### GetHwInfo (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p ADMIN -c CpuOnDemand --action GetHwInfo --cpu_id 0 --file hwidfile.txt

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p ADMIN -c CpuOnDemand --action GetHwInfo --file hwidfile.txt
```

The format of `hwidfile.txt` is `<BMC_MAC>;<CPU_ID>;<PPIN>`, for example:
```
00:30:48:00:10:12;0;AABBCCDD00112233
```

This file can be used in the GetOnDemandState action with the `--hw_id_file` option.

### GetOnDemandState (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p ADMIN -c CpuOnDemand --action GetOnDemandState --cpu_id 0 --file StateReport.json

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p ADMIN -c CpuOnDemand --action GetOnDemandState --cpu_id 0 --file StateReport.txt --squash

[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p ADMIN -c CpuOnDemand --action GetOnDemandState --cpu_id 0 --plain_text
```

### GetOnDemandState (In-Band)
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p ADMIN -c CpuOnDemand --action GetOnDemandState --hw_id AABBCCDD00112233 --file DebugStateReport.json -v
```

### GetOnDemandState (Multiple Systems OOB)
```bash
[SAA_HOME]# ./saa -l SList.txt -c CpuOnDemand --action GetOnDemandState --file mlist_report.txt
```

The system list file for `GetOnDemandState`, `SetLicenseActivateCode`, and `EnablePPIN` requires a PPIN appended to each row. If a system has more than one CPU, each PPIN must appear on its own line for that system. Two formats are supported:

```
Format 1: BMC_IP_or_HostName PPIN
Format 2: BMC_IP_or_HostName Username Password PPIN
```

`-u` and `-p` are required on the command line for Format 1. They can be omitted for Format 2, in which case the username/password in the system list file overrides the command-line `-u`/`-p` options.

`SList.txt`:
```
192.168.34.56 AABBCCDD00112233
192.168.34.57 ADMIN1 PASSWORD1 EEFFGGHH00112233
192.168.34.57 ADMIN1 PASSWORD1 EEFFGGHH00445566
```

### SetLicenseActivateCode (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p ADMIN -c CpuOnDemand --action SetLicenseActivateCode --lac_file LAC+_AABBCCDD00112233.txt --reboot
```

The format of `LAC+_AABBCCDD00112233.txt` is `<PPIN>;<LAC+ structure>`, for example:
```
AABBCCDD00112233;{"LACPlus":[...]}
```

### SetLicenseActivateCode (In-Band)
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p ADMIN -c CpuOnDemand --action SetLicenseActivateCode --lac_file LAC+_AABBCCDD00112233.txt --reboot
```

### EnablePPIN (OOB)
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p ADMIN -c CpuOnDemand --action EnablePPIN --reboot --post_complete
```

### EnablePPIN (In-Band)
```bash
[SAA_HOME]# ./saa -I Redfish_HI -u ADMIN -p ADMIN -c CpuOnDemand --action EnablePPIN --reboot
```

The system list file format for `EnablePPIN` is the same as for action 1 = GetHwInfo.

## Output

### GetHwInfo
```
Hardware type | Index | ID type | Hardware ID | Vendor | SDSi Enabled
 CPU | 0 | PPIN | AABBCCDD00112233 | GenuineIntel | YES
File "hwidfile.txt" is created.
```

### GetOnDemandState (JSON, squashed)
```
Start reading the state report on CPU 0 of 192.168.34.56 system...
.................
State Report has been successfully saved to the file <StateReport__AABBCCDD00112233.json>.
{
 "hardwareComponentData" :
 [
 {
 "hardwareId" :
 {
 "type" : "PPIN",
 "value" : "AABBCCDD00112233"
 },
 "hardwareType" : "CPU",
 "stateCertificate" :
 {
 "pendingCapabilityActivationPayloadCount" : 0,
 "value" : "AaaaaBbbbbCcccc"
 }
 }
 ],
 "objectId" : "496E74656C5F5F5352",
 "syntaxVersion" : "1.0",
 "timestamp" : "2022-09-08T14:16:03+0800"
}
```

The `--squash` variant produces a flattened, single-line record per PPIN:
```
AABBCCDD00112233;{"hardwareComponentData":[{"hardwareId":{"type":"PPIN","value":"AABBCCDD00112233"},"hardwareType":"CPU","stateCertificate":{"pendingCapabilityActivationPayloadCount":0,"value":"AaaaaBbbbbCcccc"}}],"objectId":"496E74656C5F5F5352","syntaxVersion":"1.0","timestamp":"2022-09-22T15:28:48+0800"}
```

### GetOnDemandState (verbose, `-v`)
```
Start reading the state report on CPU 0 of 192.168.34.56 system...
NVRAM capacity: 4024 B.
NVRAM used: 292 B (7.26%).
User message:
 - SDSi license auth failure count = 0
 - SDSi license auth failure treshold = 2
 - SDSi license key auth failure = 0
 - SDSi license key auth failure treshold = 2
 - SDSi updates available = 2
 - SDSi updates treshold = 2
Currently active:
 - SGX 512 EPC
Active after reboot:
```

### SetLicenseActivateCode
```
Start writing new LAC+ file on CPU 1 of 192.168.34.56 system...
...
New LAC+ file has been set successfully and is pending activation.
Status: The managed system 192.168.34.56 is rebooting.
.....................................Done
WARNING: Without option --post_complete, please manually confirm the managed system is POST complete before executing next action.
```

### EnablePPIN
```
Status: The managed system 192.168.34.56 is waiting for POST complete
....................
Status: The managed system 10.184.16.102 is POST completed
```

## Notes

- Downloading the DCL (Dear Customer Letter) for a given SKU requires an Intel RDC (Resource & Documentation Center) account.
- For On Demand Capabilities-supported CPU SKUs, contact your sales representative.
- Without `--post_complete`, you must manually confirm the managed system has completed POST before executing the next step in the flow.
