# Prompt

Configures which items are displayed in the current status prompt of the managed system while in Shell Mode. In-band only. The configuration is stored in the `saa_prompt.properties` file, located in the SAA_HOME directory, and recalled at the next startup.

## Syntax

### In-Band
```
saa -c Prompt --action <action> --item <prompt item> [--enable | --disable]
```

## Actions

- **Get**: Gets the prompt value for the given prompt item.
- **Set**: Sets the prompt value for the given prompt item.

## Options

- `--item <item name>`: Gets/Sets the prompt value for the given prompt item. Values: `all`, `time`, `fwver`, `username`, `ip`, `mb`, `power`, `acpi`.
- `--action <action>`: Sets action to Get or Set.
- `--enable` (Optional): Enables the prompt value for the specified prompt item.
- `--disable` (Optional): Disables the prompt value for the specified prompt item.

## Examples

### In-Band
```bash
[SAA_HOME]# ./saa -c Prompt --action Get --item all
```

```bash
[SAA_HOME]# ./saa -c Prompt --action Set --item time --disable
```

```bash
[SAA_HOME]# ./saa -c Prompt --action Get --item time
```

## Output

### Shell Mode Session with Prompt Enabled
```
ADMIN@192.168.34.56 X13SEI-TF/-F (S0/G0 Working,92w,01.01.05) 16:39
X13_RoT2.0_ATEN_AST2600_1_1> GetBmcInfo
Managed system...........192.168.34.56
 BMC UFFN.............BMC_X13AST2600-ROT-C301MS_20231004_01.01.05_STDsp.bin
 BMC type.............X13_RoT2.0_ATEN_AST2600_1_1
 BMC version..........01.01.05
 BMC ext. version.....01 00 00 (P)
 BMC build date.......2023/10/04
ADMIN@192.168.34.56 X13SEI-TF/-F (S0/G0 Working,117w,01.01.05) 16:39
X13_RoT2.0_ATEN_AST2600_1_1> GetBiosInfo
Managed system..........................192.168.34.56
 Board ID............................1C56
 BIOS build date.....................2023/09/18
 BIOS version........................1.5
ADMIN@192.168.34.56 X13SEI-TF/-F (S0/G0 Working,83w,01.01.05) 16:39
X13_RoT2.0_ATEN_AST2600_1_1> exit
Bye~
prompt_time: on
prompt_fwVer: on
prompt_username:on
prompt_ip: on
prompt_mb_name: on
prompt_powerW: on
prompt_acpi: on
```

### Get/Set of a Single Item
```
Prompt status for time is set for saa_prompt.properties.
prompt_time: off
```

## Notes

- The prompt fields shown correspond to: (A) Username, (B) IP address, (C) Motherboard, (D) ACPI status, (E) Power consumption, (F) IPMI firmware version, (G) Current time, (H) IPMI firmware type.
- If a prompt item does not display even when set to "on," SAA is unable to retrieve the corresponding data.
