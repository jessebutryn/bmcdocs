# ServiceCalls

Checks the system event log and sensor data record of the managed system against a ServiceCalls configuration file. After execution, the recipients assigned in the file receive SEL and SDR reports by e-mail.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c ServiceCalls {--file <servicecalls XML file>}
```

### In-Band
```
saa -c ServiceCalls {--file <servicecalls XML file>}
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c ServiceCalls {--file <servicecalls XML file>}
```

## Options

- `--file <file name>`: Monitors the host with the given XML-style file listing system event logs and sensor data records to be monitored.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c ServiceCalls --file servicecalls_sample.xml
```

### In-Band
```bash
./saa -c ServiceCalls --file servicecalls_sample.xml
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c ServiceCalls --file <servicecalls XML file>
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

If the execution "Status" field for a managed system is SUCCESS, the utilization status of the managed system is shown in the "Execution Message" section in the created log file.

## Notes

- A ServiceCalls XML file is composed of several nodes. A complete example, `servicecalls_sample.xml`, is bundled in the SAA release package.
- `<SMTPServer>` (required): SMTP server information, including the full SMTP URI (`ServerURI`) and port (`ServerPort`). SAA supports SMTP, SMTP SSL, and SMTP STARTTLS on ports 25, 465, and 587, plus the sender's e-mail address, ID, and password.
- `<Trigger_Items>`: Selects which items to monitor via three sub-nodes:
    - `SDR_Trigger_Items`: Enable or disable monitoring of Sensor Data Records.
    - `SEL_Trigger_Items`: Monitors System Event Log entries at three severities (critical, warning, information); each SEL item can be set to "Trigger" or "Skip". All SEL items are listed in `servicecalls_example.xml`.
    - `HW_Event_Alert`: Monitors HW-related SDR/SEL events (e.g. FAN mode, Power Unit Status, Memory, Drive Slot, Bus Fatal Error, DIMM Error). If "Notification" is Enable and "RecipientEmail" is valid, HW event status is e-mailed to that recipient. The default recipient e-mail is `hwevent_alert@supermicro.com`.
- `<Recipient_Information>` (required): The recipient's name, role/title, and e-mail address for non-HW event alerts.
- `<Customer_Information>`: Information about the customer applying for the ServiceCalls service.
- `<Site_Location_Information>`: The location of the managed system, including company name, address, and contact information.
- The SMTP URI in `<ServerURL>` requires a scheme: `smtp://<SMTP server path>` for plain SMTP, `smtps://<SMTP server path>` for SMTP SSL. If using `smtps`, ensure the SMTP server's SSL is enabled and its certificate is not expired.
- Only the contents of each attribute and node may be edited, and attribute content must be quoted with double quotes.
- The e-mail content includes a subject line (Event ID, function name, managed system BMC/CMM IP, host summary) and a body with e-mail function name, host IP, Event ID (32-byte GUID), and event source (OS IP of the managing system).
- Problematic items (SEL/SDR) include index, severity, timestamps, sensor type, and description; new items are marked `[NEW]`. SEL problems use three severities: critical, warning, information. SDR items exceeding their thresholds are treated as problematic. HW Event Alert e-mails always report HW-related SEL/SDR events as "Critical."
- Recovered Items (Last Check) lists SEL/SDR items previously marked problematic that have since recovered. The Summary section totals problematic and recovered items.
- Device Info shows BMC or CMM hardware information (Motherboard, System, Product Key); the information available depends on the managed system's device configuration.
- After running `ServiceCalls`, a file named `.servicecalls.cache.db` is generated in the execution folder to track SEL/SDR/HW event status between runs. Its location can be changed in the `.saarc` file. Removing the database causes a new one to be generated on the next run, and all previously problematic events are treated as new.
- Both node product keys "SFT-DCMS-SINGLE" and "SFT-DCMS-SVCKEY" are required to execute this command.
- Known limitation: SAA cannot access cache files on mounted file systems.
