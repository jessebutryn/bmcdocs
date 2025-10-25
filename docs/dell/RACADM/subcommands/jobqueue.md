# jobqueue

## Description

Enables you to view and delete a job or jobs in the current Job Queue.

**Notes:**
- Requires Server control privilege
- If unexpected error occurs, delete some jobs and retry
- Use `jobqueue create` after applying pending device configuration
- Multi-object Set commands with XML/JSON automatically create jobs

## Synopsis

- View all: `racadm jobqueue view`
- View specific: `racadm jobqueue view -i<jobid>`
- Delete specific: `racadm jobqueue delete -i<jobid>`
- Delete all: `racadm jobqueue delete --all`
- Create job: `racadm jobqueue create <fqdd> [-r <reboot type>] [-s <start time>] [-e <expiry time>]`
- Create realtime job: `racadm jobqueue create <fqdd> [-r <reboot type>] [-s <start time>] [-e <expiration time>] --realtime`

## Input

- `-i` — Job ID to display or delete (JID_CLEARALL forces delete all)
- `--all` — Delete non-applicable job IDs
- `<fqdd>` — FQDD for job creation
- `-r <reboot type>` — Reboot type:
  - `none` — No reboot (default)
  - `pwrcycle` — Power cycle
  - `graceful` — Graceful reboot without forced shutdown
  - `forced` — Graceful reboot with forced shutdown
- `-s <start time>` — Start time in yyyymmddhhmmss format (TIME_NOW = immediate, Next Reboot = until manual restart)
- `-e <expiry time>` — Expiry time in yyyymmddhhmmss format (TIME_NA = no expiry)
- `--realtime` — Real time job (for PERC 9+ controllers, no -r option)

## Examples

- View all jobs: `racadm jobqueue view`
- View specific job: `racadm jobqueue view -i <JobID>`
- Create realtime job for RAID: `racadm jobqueue create RAID.Slot.3-1 --realtime`
- Delete all jobs: `racadm jobqueue delete --all`
- Delete specific job: `racadm jobqueue delete -i <JobID>`
- Clear all jobs: `racadm jobqueue delete -i JID_CLEARALL`
- Create job with reboot: `racadm jobqueue create NIC.Integrated.1-1 -r pwrcycle -s TIME_NOW -e 20120501100000`