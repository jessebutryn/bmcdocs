# TUI

SAA supports a text-based user interface (TUI) that makes editing BIOS settings more user-friendly, with better visibility and a lower learning curve than editing an XML file directly. System configurations can be rendered with a TUI-style BIOS setup experience. It supports Linux, Windows, and FreeBSD.

Key features:

- **Easy Operation** — the visual menu makes information display more intuitive than an XML file. Users can make changes without learning the underlying rules; for example, when a function is disabled, all dependent settings become invalid or meaningless, and the TUI hides them accordingly.
- **Real-Time Feedback** — SAA validates input format in real time. When a data constraint is violated, an error message pops up immediately, without waiting for command execution to complete.
- **GUI-Free Environment** — most Unix-like servers don't have GUI packages installed. TUI provides an interactive interface on text-based systems without requiring one.
- **Automatic Configuration of Terminal Settings** — terminal settings are configured automatically to ensure display quality.

## TUI General Reminders

- The TUI feature is not supported by any terminal multiplexer.
- Do not resize the terminal display while executing a command with the `--TUI` option.
- SAA automatically configures your terminal settings for optimal display:

| Operating System | Environment Variable | Variable Value |
|---|---|---|
| Windows | code page | 437 (US English) |
| Linux | `TERM` | Linux |
| FreeBSD | `TERM` | Linux |

- After exiting the TUI, your original terminal settings are automatically restored. If restoration fails, locate and run the shell script `restore_terminal_config.sh` in the current working directory:

    Linux and FreeBSD:
    ```bash
    [shell]# source restore_terminal_config.sh
    ```

    Windows:
    ```
    X:\working directory> restore_terminal_config.bat
    ```

- On Windows, adjust the font size manually if it is too small to operate comfortably.
- The TUI does not support mouse operation.
- On FreeBSD, when running on a local terminal with a `vt` driver (the default driver after FreeBSD 11), SAA changes the font to `tui.fnt` on entering the TUI and restores the default font on exit. Rename or remove `ExternalData/tui.fnt` to disable this behavior. (`ExternalData/tui.fnt` is converted from `terminus-u12n.bdf` via `vtfontcvt`; see Appendix D of the SAA User's Guide for license details.)

## BIOS TUI Configuration

### TUI Display

SAA's TUI simulates a BIOS setup design with a display dimension of 30 rows by 100 columns. If SAA cannot resize the terminal with the current settings, it tries changing the font type and size for optimal display. Commands to change terminal dimensions manually:

| Operating System | Command to Change Terminal Dimensions |
|---|---|
| Windows | `mode con lines=30 cols=100` |
| Linux | `stty cols 100 rows 30` |
| FreeBSD (`sc` driver, local host) | Change console video mode with `vidcontrol` |
| FreeBSD (`vt` driver, local host) | Change console font with `vidcontrol -f` |
| FreeBSD (remote console) | `stty cols 100 rows 30` |

Terminal dimensions are automatically changed, which may also change some settings.

!!! note
    The `GetCurrentBiosCfg` command is supported for retrieving the resulting BIOS configuration. See [Getting Current BIOS Settings](bios/getcurrentbioscfg.md) for details.

### How to Use

**Using Arrow Keys** — when SAA's BIOS Setup Utility is first entered, the "Main" root menu appears. Press `<RIGHT>` and `<LEFT>` to navigate between menu tabs.

**Setting Values** — a `+` symbol before an option indicates a sub-menu can be expanded for further configuration. Press `<+>` and `<->` to change a setting value, or press `<Enter>` to open a dialog box for configuration. Some settings and requirements may vary across different BIOS systems where the TUI runs.

**Using a Check Box to Enable/Disable a Function** — press `<Enter>` to open a dialog box, then use `<UP>` and `<DOWN>` to make a selection. Select "Unchecked" to disable a function, or "Checked" to enable it.

**Setting Numeric Values** — a value may be limited by the BIOS. Press number keys to enter the desired value directly, or use `<+>` and `<->` to adjust it within the allowed range. If an input value is invalid, a warning message appears.

### Getting General Help

Press `<F1>` for general help information. A message box appears.

### Loading Previous Values

Press `<F2>` to load the previous values for all configurations. A confirmation message appears.

### Loading Optimized Values

Press `<F3>` to return all configurations to their default values. A confirmation message appears.

### Setting a Password

Go to **Security**, select **Administrator Password**, and press `<Enter>` to set a password.

- If a password is already set in the BIOS, a series of three asterisks appears on the Security page to indicate this.
- The allowed password length may vary depending on the BIOS in use — for example, some BIOS versions accept passwords from 3 to 20 characters long.

### Exiting the TUI

Two ways to exit the SAA BIOS configuration TUI:

- **Without saving** — press `<ESC>`. A confirmation message appears. This only works from the root menu; pressing `<ESC>` in a submenu returns to the previous menu instead.
- **Saving and exiting** — press `<F4>`. A confirmation message appears.
