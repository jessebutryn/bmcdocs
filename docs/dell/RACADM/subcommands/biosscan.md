# biosscan

## Description

Allows iDRAC to scan the BIOS on scheduled intervals or as requested by the user.

## Synopsis

- Schedule: `racadm biosscan -s <Frequency Type>`
- Or: `racadm biosscan -s <frequency> -t <start-time> -d <start-date>`

## Input

- `-s` — Schedule type:
  - 0: Never schedule and delete existing schedules
  - 1: Schedule now
  - 2: Schedule daily
  - 3: Schedule weekly
  - 4: Schedule monthly
  - 5: Schedule yearly
- `-t <HH:00>` — Start time in 24-hour format (minutes must be 00). Default: 23:00
- `-d <YYYY-MM-DD>` — Start date. Default: current date

**Notes:**
- `-t` and `-d` must be specified together, not applicable for -s 0 and -s 1
- In modular systems, scheduled start time (minutes) may vary based on server slot number

## Examples

- Scan immediately: `racadm biosscan -s 1`
- Daily scan: `racadm biosscan -s 2`
- Weekly scan at 21:00 from Dec 20, 2020: `racadm biosscan -s 3 -t 21:00 -d 2020-12-20`
- Weekly from today at default time: `racadm biosscan -s 3`