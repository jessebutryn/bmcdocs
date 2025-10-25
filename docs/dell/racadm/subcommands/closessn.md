# closessn

## Description

Closes a communication session on the device. Use `getssninfo` to view a list of sessions that can be closed.

To run this subcommand, you must have the Administrator permission.

**Note:** This subcommand ends all the sessions other than the current session.

## Synopsis

- Close specific session: `racadm closessn –i <session_ID>`
- Close all sessions: `racadm closessn -a`
- Close sessions for user: `racadm closessn -u <username>`

## Input

- `-i <session_ID>` — The session ID to close (retrieved using `getssninfo`). Cannot close the current session.
- `-a` — Closes all sessions.
- `-u <username>` — Closes all sessions for a particular user name.

## Output

Successful or error message is displayed.

## Examples

- Close session 1234: `racadm closessn -i 1234`
- Close all sessions for root: `racadm closessn –u root`
- Close all sessions: `racadm closessn –a`