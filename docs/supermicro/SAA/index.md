# SAA (SuperServer Automation Assistant)

The SuperServer Automation Assistant (SAA) is Supermicro's command-line tool for managing Supermicro systems. It helps IT administrators manage firmware image updates and configuration updates across a system's firmware — including BIOS, BMC, CMM, PSU, BBP, RAID, AOC NIC, GPU, switch, AIP, and SCP — and supports system checks and event log management. To update configurations, users can edit system BIOS configurations, DMI information, and BMC/RAID/CMM configurations from readable text files, then apply them with SAA.

SAA supports Redfish, IPMI, or both, depending on the BMC generation of each platform. Systems can be managed remotely through an out-of-band (OOB) channel, or locally through an in-band channel, with one-to-many configuration management for mass deployment.

## Getting Started

- [Overview](overview.md) — architecture, supported features, and operational requirements
- [Installation and Setup](installation.md) — installing SAA and preparing managed systems for OOB, in-band, remote in-band, and VROC usage
- [Licensing Managed Systems](licensing.md) — activating and managing node product keys
- [Basic Usage](basic-usage.md) — command syntax, connection options, and SAA configuration
- [Logs](logs.md) — log file locations and formats

## Reference

- [XML File Formats](xml-file-formats.md) — BIOS, BMC, BMC LAN, CMM, RAID, VROC, TwinPro, and Fixed Boot configuration XML schemas
- [Text File Formats](text-file-formats.md) — DMI information text file format
- [TUI](tui.md) — the text-based user interface for BIOS configuration

## Command Reference by Category

- [Applications](applications/) — IPMI raw commands, USB access mode, KMS server configuration, Redfish API calls, remote shell, SOL, BMC discovery, and SAA shell mode
- [BIOS Management](bios/) — BIOS updates, configuration, DMI information, passwords, SCP, and fixed boot order
- [BMC Management](bmc/) — BMC updates, configuration, LAN settings, users, KCS privilege, watchdog, and SNMP
- [CMM Management](cmm/) — CMM and BBP updates, configuration, power control, profiles, switch firmware, and PSU management
- [CPLD Management](cpld/) — CPLD firmware for motherboard, switchboard, backplane, fanboard, AIP, AOM, and related components
- [FPGA Management](fpga/) — motherboard FPGA information and updates
- [GB200 Certificate Management](gb200cert/) — certificate management for NVIDIA GB200 systems
- [GPU Management](gpu/) — GPU information, firmware updates, diagnostics, logs, and power limits
- [Health Management](health/) — capabilities, asset information, utilization, sensors, event/SDR monitoring, predictive failure analysis, diagnostics, and CDU monitoring
- [License Management](license/) — activating and querying node product keys and CPU On Demand capabilities
- [MCU Management](mcu/) — motherboard MCU information and updates
- [Multi-Node Management](multinode/) — TwinPro configuration and multi-node EC/LCMC updates
- [NIC Management](nic/) — AOC NIC firmware information and updates
- [NM Management](nm/) — Intel Management Engine, Node Manager, CPU, and CUPS management
- [PCIe-Switch Management](pcieswitch/) — PCIe switch firmware information and updates
- [Power Management](power/) — PSU information and updates, power status/actions, DCMI, power policy, ACPI, AIOM standby power, and CPU power limits
- [Security Management](security/) — RoT functions, Secure Boot, system lockdown, attestation, secure erase, TPM, CPU/GPU ERoT, and SPDM measurements
- [Storage Management](storage/) — RAID controller, SATA/NVMe/PMem information, VROC, and SAS Expander management
- [System Management](system/) — FRU information, system summaries, BIOS/BMC configuration, fan configuration, UID, firmware inventory, and CMOS clear
- [System Event Log](systemeventlog/) — event log and maintenance event log retrieval/clearing, crash dumps, and SEL time
- [VM Management](vm/) — virtual media mounting and management
