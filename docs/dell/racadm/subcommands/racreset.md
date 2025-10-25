# racreset

## Description

Resets iDRAC. The reset event is logged in the iDRAC log.

To run this subcommand, you must have the Configure iDRAC privilege and configure user privilege.

NOTE: After you run the racreset subcommand, iDRAC may require up to two minutes to return to a usable state.

## Synopsis

```
racadm racreset soft
racadm racreset hard
racadm racreset soft -f
racadm racreset hard -f
```

## Input

- `-f` — This option is used to force the reset.

## Output/Example

iDRAC reset

```
racadm racreset
```

```
RAC reset operation initiated successfully. It may take up to a minute
for the RAC to come online again.
```