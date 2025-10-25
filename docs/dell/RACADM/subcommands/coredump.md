# coredump

## Description

Displays detailed information related to any recent critical issues that have occurred with iDRAC. The coredump information can be used to diagnose these critical issues.

If available, the coredump information is persistent across iDRAC power cycles and remains available until deleted using the `coredumpdelete` subcommand.

**Note:** Requires Execute Debug privilege.

## Synopsis

```bash
racadm coredump
```

## Input

None

## Output

Displays coredump information if available, or "There is no coredump currently available."

## Example

```bash
racadm coredump
# Output: Feb 19 15:51:40 (none) last message repeated 5 times
#         Feb 19 15:52:41 (none) last message repeated 4 times
#         ...
```