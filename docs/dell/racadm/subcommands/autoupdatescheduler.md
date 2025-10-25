# autoupdatescheduler

## Description

You can automatically update the firmware of the devices on the server.

To run this subcommand, you must have the Server Control privilege.

**Notes:**
- The autoupdatescheduler subcommand can be enabled or disabled.
- Lifecycle Controller and CSIOR may not be enabled to run this subcommand.
- The minimum Lifecycle Controller version required is Lifecycle Controller 1.3.
- When a job is already scheduled and the clear command is run, the scheduling parameters are cleared.
- If the network share is not accessible or the catalog file is missing when the job is scheduled, then the job is unsuccessful.

## Synopsis

- To create the AutoUpdateScheduler: `racadm autoupdatescheduler create -u <user> -p <password> -l <location> -f <filename> -time <time> -dom <DayOfMonth> -wom <WeekOfMonth> -dow <DayofWeek> -rp <repeat> -a <applyreboot> -ph <proxyHost> -pu <proxyUser> -pp <proxyPassword> -po <proxyPort> -pt <proxyType>`
- To view AutoUpdateScheduler parameter: `racadm autoupdatescheduler view`
- To clear and display AutoUpdateScheduler parameter: `racadm autoupdatescheduler clear`

**Note:** After the parameters are cleared, the AutoUpdateScheduler is disabled. To schedule the update again, enable the AutoUpdateScheduler.

## Input

- `-u` — Specifies the user name of the remote share that stores the catalog file. (For CIFS, enter the domain name as domain or username.)
- `-p` — Specifies the password of the remote share that stores the catalog file.
- `-l` — Specifies the network share (NFS, CIFS, FTP, TFTP, HTTP, or HTTPS) location of the catalog file. IPv4 and IPv6 addresses are supported.
- `-f` — Specifies the catalog location and the filename. If the filename is not specified, then the default file used is catalog.xml.
- `-ph` — Specifies the FTP/HTTP proxy host name.
- `-pu` — Specifies the FTP/HTTP proxy user name.
- `-pp` — Specifies the FTP/HTTP proxy password.
- `-po` — Specifies the FTP/HTTP proxy port.
- `-pt` — Specifies the FTP/HTTP proxy type.
- `-time` — Specifies the time to schedule an autoupdate in the HH:MM format. This option must be specified.
- `-dom` — Specifies the day of month to schedule an autoupdate. Valid values are 1–28, L (Last day) or '*' (default — any day).
- `-wom` — Specifies the week of month to schedule an autoupdate. Valid values are 1–4, L (Last week) or '*' (default — any week).
- `-dow` — Specifies the day of week to schedule an autoupdate. Valid values are sun, mon, tue, wed, thu, fri, sat, or '*' (default — any day).
- `-rp` — Specifies the repeat parameter. This parameter must be specified.
  - If the-dom option is specified, then the valid values for -rp are 1–12.
  - If the-wom option is specified, then the valid values for -rp are 1–52.
  - If the-dow option is specified, then the valid values for -rp are 1–366.
- `-a` — Applies reboot (1 — Yes, 0 — No). This option must be specified.

## Examples

- For CIFS: `racadm autoupdatescheduler create -u domain/admin -p xxx -l //1.2.3.4/share -f cat.xml -time 14:30 -wom 1 -dow sun -rp 1 -a 1`
- For NFS: `racadm autoupdatescheduler create -u nfsadmin -p nfspwd -l 1.2.3.4:/share -f cat.xml -time 14:30 -dom 1 -rp 5 -a 1`
- For FTP: `racadm autoupdatescheduler create -u ftpuser -p ftppwd -l ftp.test.com -f cat.xml.gz -ph 10.20.30.40 -pu padmin -pp ppwd -po 8080 -pt http -time 14:30 -dom 1 -rp 5 -a 1`
- For HTTP: `racadm autoupdatescheduler create -u httpuser -p httppwd -l http://test.com -f cat.xml -ph 10.20.30.40 -pu padmin -pp ppwd -po 8080 -pt http -time 14:30 -dom 1 -rp 5 -a 1`
- For TFTP: `racadm autoupdatescheduler create -l tftp://1.2.3.4 -f cat.xml.gz -time 14:30 -dom 1 -rp 5 -a 1`
- To view: `racadm autoupdatescheduler view`
- To clear: `racadm autoupdatescheduler clear`