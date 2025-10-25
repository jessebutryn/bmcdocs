# serveraction

## Description

Enables you to perform power management operations on the blade system.

To run this subcommand, you must have the Execute Server Control Commands permission.

## Synopsis

```bash
racadm serveraction <action> -f
```

## Input

- `<action>` — Specifies the power management operation to perform. The options are:
  - `hardreset` — Performs a force reset (reboot) operation on the managed system.
  - `powercycle` — Performs a power-cycle operation on the managed system. This action is similar to pressing the power button on the system's front panel to turn off and then turn on the system.
  - `powerdown` — Powers down the managed system.
  - `powerup` — Powers up the managed system.
  - `powerstatus` — Displays the current power status of the server (ON or OFF).
  - `graceshutdown` — Performs a graceful shutdown of the server. If the operating system on the server cannot shut down completely, then this operation is not performed.
  - `nmi` — Generates the Non-masking interrupt (NMI) to halt the system operation. The NMI sends a high-level interrupt to the operating system, which causes the system to halt the operation to allow critical diagnostic or troubleshooting activities.
- `-f` — Force the server power management operation. (Applicable only for the PowerEdge-VRTX platform. Used with powerdown, powercycle, and hardreset options.)

**Note:** The action `powerstatus` is not allowed with `-f` option.

## Output

Displays an error message if the requested operation is not completed, or a success message if the operation is completed.

## Examples

- Get Power Status: `racadm serveraction powerstatus`
  - Output: `Server Power Status: ON`
- Power Cycle: `racadm serveraction powercycle`
  - Output: `Server power operation successful`