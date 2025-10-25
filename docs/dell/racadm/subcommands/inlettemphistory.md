# inlettemphistory

## Description

Displays the average and the peak temperatures during the last hour, day, week, month, or year. Also exports the inlet temperature history data file. The file can be exported to a remote file share, local file system, or the management station.

NOTE: For FM120x4 systems, this subcommand provides the historical data for system board temperature.

## Synopsis

```
racadm inlettemphistory get
racadm inlettemphistory export -f <Filename> -u <username> -p <password> -l <location> -t <export file type>
```

## Input

- `-f` — Exports inlet temperature history filename. The maximum length of this parameter is 64 characters.
- `-u` — User name of the remote share to export the file. Specify user name in a domain as domain or username.
- `-p` — Password for the remote share to where the file must be exported.
- `-l` — Network share location to where the inlet temperature history must be exported. The maximum length of this parameter is 256 characters.
- `-t` — Specifies the exported file type. Valid values are xml and csv. These values are case-insensitive.

## Output/Example

Export the log to a remote CIFS share.

```
racadm inlettemphistory export -f Mylog.xml -u admin -p xxx -l //1.2.3.4/share -t xml
```

Export the log to a remote HTTP share.

```
racadm inlettemphistory export -f Mylog.xml -u httpuser -p httppwd -l http://test.com -t xml
```

Export the log to a remote HTTPS share.

```
racadm inlettemphistory export -f Mylog.xml -u httpsuser -p httpspwd -l https://test.com -t xml
```

Export the log to a remote NFS share.

```
racadm inlettemphistory export -f Mylog.csv -l 1.2.3.4:/home/user -t csv
```

Export the log to a remote FTP share.

```
racadm inlettemphistory export -f Mylog.csv -u ftpuser -p ftppwd -l ftp://test.com/share -t csv
```

Export the log to a remote TFTP share.

```
racadm inlettemphistory export -f Mylog.csv -l tftp://test.com/share -t csv
```

Export the log to local file system using Local RACADM.

```
racadm inlettemphistory export -f Mylog.xml -t xml
```

Export the log to management station using Remote RACADM.

```
racadm -r 1.2.3.4 -u user -p xxx inlettemphistory export -f Mylog.csv -t csv
```

View the inlet temperature history.

```
racadm inlettemphistory get
Duration Above Warning Threshold as Percentage = 0.0%
Duration Above Critical Threshold as Percentage = 0.0%
Average Temperatures
Last Hour = 23C ( 73.4F )
Last Day = 24C ( 75.2F )
Last Week = 24C ( 77.0F )
Last Month = 25C ( 77.0F )
Last Year = 23C ( 73.4F )
Peak Temperatures
Last Hour = 23C ( 73.4F ) [At Wed, 21 May 2017 11:00:57]
Last Day = 25C ( 77.0F ) [At Tue, 21 May 2017 15:37:23]
Last Week = 27C ( 80.6F ) [At Fri, 20 May 2017 10:38:20]
Last Month = 29C ( 84.2F ) [At Wed, 16 May 2017 15:34:13]
Last Year = 29C ( 84.2F ) [At Wed, 16 May 2017 15:34:13]
```