# coredumpdelete

## Description

Deletes any currently available coredump data stored in the RAC.

**Note:** Requires Execute Debug Command permission. If no coredump exists, still shows success message.

## Synopsis

```bash
racadm coredumpdelete
```

## Input

None

## Output

Success message indicating coredump deletion.

## Example

```bash
racadm coredumpdelete
# Output: Coredump is deleted.
# Or: Coredump request completed successfully
```