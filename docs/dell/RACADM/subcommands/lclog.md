# lclog

## Description

Allows you to:

- Export the lifecycle log history. The log exports to remote or local share location.
- View the lifecycle log for a particular device or category
- Add comment to a record in lifecycle log
- Add a work note (an entry) in the lifecycle log
- View the status of a configuration job.

NOTE:

- When you run this command on Local RACADM, the data is available to RACADM as a USB partition and may display a pop-up message.
- While Lifecycle Controller is running for racadm commands, you cannot perform other operation which needs Lifecycle Controller Partition. If the Lifecycle Controller Partition is unreleased (because of improper closure of racadm command in the partition), then you must wait 20-35 minutes to clear the Lifecycle Controller Partition

## Synopsis

```bash
racadm lclog comment edit –q <sequence number> -m <Text to be added>
racadm lclog view -i <number of records> -a <agent id> -c <category> -s <severity> -b <sub-category> -q <sequence no> -n <number of records> -r <start timestamp> -e <end timestamp>
racadm lclog export -f <filename> -u <username> -p <password> -l <CIFS or NFS or HTTP or HTTPS or TFTP or FTP share>
racadm lclog export -f <filename> -u <username> -p <password> -l <CIFS or NFS or HTTP or HTTPS or TFTP or FTP share> --complete
racadm -r <idracip> -u <idrac username> -p <idrac password> lclog export -f <filename> -u <username> -p <password> -l <CIFS or NFS or HTTP or HTTPS or TFTP or FTP share>
racadm -r <idracip> -u <idrac username> -p <idrac password> lclog export -f <filename> -u <username> -p <password> -l <CIFS or NFS or HTTP or HTTPS or TFTP or FTP share> --complete
racadm lclog viewconfigresult -j <job ID>
racadm lclog worknote add -m <text to be added>
```

## Input

- `-i` — Displays the number of records present in the active log.
- `-a` — The agent ID used to filter the records. Only one agent ID is accepted. The value is case-insensitive. Valid Agent-ID values:
  - UEFI_SS_USC
  - CusOsUp
  - UEFI_Inventory
  - iDRAC
  - UEFI_DCS
  - SEL
  - RACLOG
  - DE
  - WSMAN
  - RACADM
  - iDRAC_GUI
- `-k` — Filters the records based on the filter string provided in racadm lclog view command.
- `-c` — The category used to filter the records. Provides multiple categories using a "," as the delimiter. The value is case-insensitive. Valid category values:
  - System
  - Storage
  - Worknotes
  - Config
  - Updates
  - Audit
- `-b` — The subcategory used to filter the records. Provides multiple subcategories using a "," as the delimiter.
- `-q` — The sequence number from which the records must be displayed. Records older than this sequence number is displayed.
  - NOTE: This parameter input is an integer. If an alphanumeric input is provided, then invalid subcommand syntax error is displayed.
- `-n` — Specifies the n number of records that must be displayed. On Local RACADM, if this parameter is not specified, by default 100 logs are retrieved.
- `-r` — Displays events that have occurred after this time. The time format is yyyy-mm-dd HH:MM:SS. The time stamp must be provided within double quotation marks.
- `-e` — Displays events that have occurred before this time. The time format is yyyy-mm-dd HH:MM:SS. The time stamp must be provided within double quotation marks.
- `-f <filename>` — Specifies the file location and name where lifecycle log is exported.
- `-a <name>` — Specifies the FTP Server IP address or FQDN, user name, and password.
- `-l <location>` — Specifies the location of the network share or area on file system where lifecycle log is exported. Two types of network shares are supported:
  - SMB-mounted path: //<ipaddress or domain name>/<share_name>/<path to image>
  - NFS-mounted path: <ipaddress>:/<path to image>.
- `-u <user>` — Specifies the user name for accessing the FTP server, or Domain and user name for accessing network share location.
- `-p <password>` — Specifies the password for accessing the FTP server or share location.
- `-s` — The severity used to filter the records. Provide multiple severities using a "," as the delimiter. The value is case-insensitive. Valid Severity values:
  - Warning
  - Critical
  - Info
- `—m <Comment>` — User comment string for a record that must be inserted in the Lifecycle Controller log. This comment string must be less than 128 characters. The text must be specified within double quotation mark.
  - NOTE: HTML-specific characters may appear as escaped text.
- `-m <Worknote>` — Adds a worknote (an entry) in the Lifecycle log. This worknote must be less than 256 characters. The text must be specified within double quotation mark.
  - NOTE: HTML-specific characters may appear as escaped text.
  - NOTE: For -m <worknote> and —m <comment> options, you need test alert privilege.
- `--complete` — Export the complete Lifecycle log as a compressed file. The exported file is of the type .xml.gz.
- `-j<Job ID>` — Specifies the Job ID.

## Examples

- Display the number of records present in the Lifecycle log.
  ```bash
  racadm lclog view -i
  ```

- Display the records containing the string session
  ```bash
  racadm lclog view -k session
  ```

- Display the iDRAC agent idrac records, under the storage category and storage physical disk drive subcategory, with severity set to warning.
  ```bash
  racadm lclog view -a idrac -c storage -b pdr -s warning
  ```

- Display the records under storage and system categories with severities set to warning or critical.
  ```bash
  racadm lclog view -c storage,system -s warning,critical
  ```

- Display the records having severities set to warning or critical, starting from sequence number 4.
  ```bash
  racadm lclog view -s warning,critical -q 4
  ```

- Display 5 records starting from sequence number 20.
  ```bash
  racadm lclog view -q 20 -n 5
  ```

- Display all records of events that have occurred between 2011-01-02 23:33:40 and 2011-01-03 00:32:15.
  ```bash
  racadm lclog view -r "2011-01-02 23:33:40" -e "2011-01-03 00:32:15"
  ```

- Display all the available records from the active Lifecycle log.
  ```bash
  racadm lclog view
  ```
  NOTE: If output is not returned when this command is used remotely, then retry increasing the remote RACADM timeout value. To increase the timeout value, run the command racadm set iDRAC.Racadm.Timeout <value>. Alternatively, you can retrieve few records.

- Add a comment to record number 5 in the Lifecycle log.
  ```bash
  racadm lclog comment edit –q 5 –m "This is a test comment."
  ```

- Add a worknote to the Lifecycle log.
  ```bash
  racadm lclog worknote add -m "This is a test worknote."
  ```

- Export the complete Lifecycle log in gzip format to a remote FTP share
  ```bash
  racadm lclog export -f log.xml.gz -u ftppuser -p ftppwd –l ftp://192.168.0/share
  ```

- Export the complete Lifecycle log in gzip format to a remote TFTP share
  ```bash
  racadm lclog export -f log.xml.gz tftp://192.168.0.1/
  ```

- Export the Lifecycle log to a remote FTP share
  ```bash
  racadm lclog export -f Mylog.xml -u ftppuser -p ftppwd –l ftp://192.168.0/share
  ```

- Export the Lifecycle log to a remote TFTP share
  ```bash
  racadm lclog export -f Mylog.xml tftp://192.168.0.1/
  ```

- Export the Lifecycle log to a remote CIFS share.
  ```bash
  racadm lclog export -f Mylog.xml -u admin -p xxx -l //192.168.0/share
  ```

- Export the complete Lifecycle log in gzip format to a remote CIFS share.
  ```bash
  racadm lclog export -f log.xml.gz -u admin -p xxx -l //192.168.0/share --complete
  ```

- Export the Lifecycle log to a remote NFS share.
  ```bash
  racadm lclog export -f Mylog.xml -l 192.168.0:/home/lclog_user
  ```

- Export the Lifecycle log to a local share using Local RACADM.
  ```bash
  racadm lclog export -f Mylog.xml
  ```

- Export the complete Lifecycle log in gzip format to a local share using Local RACADM.
  ```bash
  racadm lclog export -f log.xml.gz --complete
  ```

- Export the Lifecycle log lclog to a local share using Remote RACADM.
  ```bash
  racadm -r 192.168.0 -u admin -p xxx lclog export -f Mylog.xml
  ```

- Display the status of the specified Job ID with Lifecycle Controller.
  ```bash
  racadm lclog viewconfigresult -j JID_123456789012
  ```

- Export the complete Lifecycle Log in gzip format to a remote HTTP share:
  ```bash
  racadm lclog export -f log.xml.gz -u httpuser -p httppwd -l http://test.com
  ```

- Export the complete Lifecycle Log in gzip format to a remote HTTPS share
  ```bash
  racadm lclog export -f log.xml.gz -u httpsuser -p httpspwd -l https://test.com
  ```

- Export the Life Cycle Log to a remote HTTP share
  ```bash
  racadm lclog export -f Mylog.xml -u httpuser -p httppwd -l http://test.com
  ```

- Export the Life Cycle Log to a remote HTTPS share
  ```bash
  racadm lclog export -f Mylog.xml -u httpsuser -p httpspwd -l https://test.com
  ```

NOTE: Squid proxy configuration is not supported to access http/https shares.