# ServiceCalls

Monitors the host system event log and sensor data records using a ServiceCalls configuration file and sends reports via email.

## Syntax

```
sum [-i <IP or host name> -u <username> -p <password>] -c ServiceCalls --file <servicecalls XML file>
```

## Options

- `--file <servicecalls XML file>`: Path to the ServiceCalls XML configuration file.

## Examples

### OOB
```
[SUM_HOME]# ./sum -i 192.168.34.56 -u ADMIN -p PASSWORD -c ServiceCalls --file servicecalls_sample.xml
```

### In-Band
```
[SUM_HOME]# ./sum -c ServiceCalls --file servicecalls_sample.xml
```

## ServiceCalls XML File Format

A ServiceCalls XML file contains several nodes:

### SMTP Server Node - <SMTPServer> (Required)
Contains email server information:
- `ServerURI`: Full SMTP URI (e.g., "smtp://server" or "smtps://server")
- `ServerPort`: SMTP port (25, 465, or 587)
- `SSL`: SMTP SSL support
- `STARTTLS`: SMTP STARTTLS support
- `SenderEmail`: Sender's email address
- `SenderID`: Sender's ID
- `SenderPassword`: Sender's password

### Trigger Items Node - <Trigger_Items>
Contains monitoring configuration:
- `SDR_Trigger_Items`: Enable/disable SDR monitoring
- `SEL_Trigger_Items`: SEL event types to monitor (critical, warning, information)
- `HW_Event_Alert`: Hardware event monitoring with recipient email

### Recipient Information Node - <Recipient_Information> (Required)
Contains recipient details:
- `Name`: Recipient name
- `Role`: Recipient title
- `Email`: Recipient email address

### Customer Information Node - <Customer_Information>
Contains customer information:
- Customer name and company details

### Site Location Information Node - <Site_Location_Information>
Contains location information:
- Company name, address, and contact information

## Email Format

The ServiceCalls command sends emails with the following content:

### Subject Line
Contains Event ID, function name, BMC/CMM IP, and host summary.

### Body Sections
- **Email Function**: "SUM Service Calls"
- **Host IP**: BMC/CMM IP address
- **Event ID**: 32-byte GUID
- **Event Source**: Managing system OS IP
- **Problematic Items**: SEL and SDR items that exceed thresholds
- **Recovered Items**: Previously problematic items that have recovered
- **Summary**: Count of problematic and recovered items
- **Additional Items**: Normal status SDR items or HW events
- **Device Info**: BMC/CMM hardware information
- **Site Location Info**: System location
- **Customer Info**: Customer details

## Cache File

After execution, a `.servicecalls.cache.db` file is created in the execution folder to track event status changes between runs.

## Notes

- Only the contents of attributes and nodes can be edited in the XML file.
- Attribute content must be quoted with double quotes.
- SMTP URI requires proper scheme ("smtp://" for regular SMTP, "smtps://" for SSL).
- For SMTPS, ensure the SMTP server's SSL certificate is valid and not expired.
- Both "SFT-DCMS-SINGLE" and "SFT-DCMS-SVC-KEY" node product keys are required.
- You cannot access cache files on mounted file systems with the ServiceCalls command.
- A sample configuration file "servicecalls_sample.xml" is bundled with SUM.</content>
<parameter name="filePath">/home/jesse/git/bmcdocs/docs/supermicro/sum/servicecalls.md