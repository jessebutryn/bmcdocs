# SAA Logs

While SAA commands run, log messages are recorded for issue tracking and reproduction. This page details the types of logs SAA generates.

## Command Usage History

When an SAA command is executed, the executed command with its options is automatically logged to an `saa.log` file. The root cause of an issue may result from previously executed commands, so a history of command usage makes issue investigation easier.

- Use the `-p` or `-f` option to supply a password — these two options cannot be used together.
- For concurrent execution of OOB commands across multiple systems, use the `-l` option. See [Basic User Interface](basic-usage.md#managing-multiple-systems) for details.
- Every command execution is recorded in `saa.log`. In addition, when rare exceptions occur in BMC/CMM/RAID configuration get/set commands, timestamped logs are created. If the `/var/log/supermicro/SAA` folder exists, logs are stored there; otherwise they are stored in the same folder as `$PWD` (Unix-like OS) or `%cd%` (Windows).
- For the `--reboot` option in OOB usage: if the target OS supports software shutdown and has X-Window installed on Red Hat, the system is forced to power off and then power back up. Ensure data is saved before running the SAA command — whether software shutdown is supported from the console prompt depends on the Red Hat version.
- If the system is configured to hibernate or sleep, it may hang when rebooted. To avoid this, run the following in the target OS before updating BIOS:

    ```bash
    gsettings set org.gnome.settings-daemon.plugins.power power-button-action nothing
    ```

- With the `--post_complete` option, SAA waits until the managed system's POST completes, so the system is ready for the next OOB action.

## Critical Error Log

When SAA encounters a critical error, the error message is logged automatically. Like system error logs, critical error messages are always notable and require further action.

## Multiple-System Log

When an SAA command runs in multiple-system mode (with `-l`), a multiple-system log is generated automatically. It summarizes all running results across systems, including running status (`FAILED` or `SUCCESS`), execution time, and exit codes.

## Command Execution Journal

The journal records footprint messages during command execution. Severity levels range from 0 to 6 — level 0 (silent) generates no messages, and level 6 (verbose) generates the most. Journal entries are also tagged with functional categories, such as `GENERIC` (messages that don't fit any particular category) or `CURL` (messages related to the curl library), so the journal can be filtered quickly during investigation.

By default the journal is disabled (severity level 0). Enable it with the `--journal_level` option (higher priority) or the `.saarc` configuration (lower priority). By default the journal is created in the user home directory; the `--journal_path` option (higher priority) or `.saarc` configuration (lower priority) overrides the output path.

## Log Types and Output Path Priorities

| Log Type | Activation | Output Path Priority |
| --- | --- | --- |
| Command usage history | Always activated | 1. `--journal_path` option (log exists in the "History" subfolder of the defined path) <br>2. `/var/log/supermicro/SAA` <br>3. `$PWD` (Linux) or `%cd%` (Windows) |
| Critical error log | Always activated | 1. `--journal_path` option (log exists in the "Critical" subfolder of the defined path) <br>2. `/var/log/supermicro/SAA` <br>3. `$PWD` (Linux) or `%cd%` (Windows) |
| Multiple system log | Always activated | 1. `--journal_path` option (log exists in the "Multiple" subfolder of the defined path) <br>2. `/var/log/supermicro/SAA` <br>3. Same directory as the multiple-system list file |
| Command execution journal | Activated by configuration | 1. `--journal_path` option (log exists in the defined path) <br>2. `.saarc` in the home directory <br>3. `~/journal/supermicro/saa/` (Linux) or `%HomePath%\journal\supermicro\saa\` (Windows) |
