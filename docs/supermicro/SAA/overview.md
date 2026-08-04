# Overview

The SuperServer Automation Assistant (SAA) is designed to manage Supermicro systems. It helps IT administrators easily manage firmware image updates and configuration updates on a system's firmware, including BIOS, BMC, CMM, PSU, BBP, RAID, AOC NIC, GPU, switch, AIP, and SCP. System checks and event log management are also supported. Advanced applications are provided to facilitate system management. To update configurations, users can edit system BIOS configurations, DMI information, and BMC/RAID/CMM configurations from readable text files, then use SAA to apply these configurations.

SAA supports Redfish, IPMI, or both industry standards for system management, depending on the BMC generation of each platform. Users can manage BMC-based systems remotely through the out-of-band (OOB) channel, or locally through the in-band channel. SAA also provides one-to-many configuration management for mass deployment and management.

## Features

- Command-line interfaced (CLI) and scriptable
- Independent from the OS on managed systems (for OOB usage)
- Operates through OOB (Out-Of-Band) and in-band methods
- Supports concurrent execution of OOB commands on multiple systems through a system list file

### License Management

- Activates the node product key of the managed system
- Queries the node product key of the managed system
- Gets and activates Intel(R) CPU On Demand capabilities features

### Health Management

- Gets the OOB feature capabilities of the managed system
- Gets the asset information of the managed system
- Gets the utilization rates of the managed system components
- Gets the IPMI sensor values of the managed system
- Monitors the status of the system event log and sensor data record of the managed system
- Monitors and controls the predictive failure analysis of the managed system
- Sets the memory health checking function of the managed system
- Gets and clears the chassis intrusion status for the managed system
- Gets and queries SNMP trap messages
- Runs Super Diagnostics Offline (SDO) and checks results
- Sends Diag Interrupt
- Monitors CDU system to get status and set settings remotely
- Executes TAS-related actions
- Checks and reports the basic health status of the BMC
- Gets and sets the hardware debug tool status

### System Management

- Gets the FRU information of the managed system/input dumped FRU file
- Restores dumped FRU info to the managed system
- Updates FRU information
- Obtains a summary of information from the managed system
- Gets the system configuration (BIOS and BMC) of the managed system
- Updates the system configuration (BIOS and BMC) of the managed system
- Gets the fan configuration of the managed system
- Sets the fan configuration of the managed system
- Executes commands to control UID
- Obtains a summary of Firmware Inventory information from the managed system
- Executes the command to clear the CMOS

### BIOS Management

- Updates BIOS
- Gets the BIOS information of the managed system/input BIOS image file
- Gets the default factory BIOS configuration of the managed system
- Gets the current BIOS configuration of the managed system
- Updates the BIOS configuration
- Loads the default factory BIOS configuration
- Gets the DMI information of the managed system
- Edits the given DMI information text file
- Updates DMI information
- Sets the BIOS Administrator password
- Erases the OA key of the managed system
- Gets the SCP information of the managed system
- Updates SCP
- Gets the BIOS fixed boot order configuration of the managed system
- Gets BMC boot information
- Sets BMC boot status
- Boots into an ISO image from the image file server
- Updates the BIOS fixed boot order
- Gets BIOS POST code

### BMC Management

- Updates BMC
- Gets the BMC information of the managed system/input BMC image file
- Gets the BMC configuration of the managed system
- Updates the BMC configuration
- Gets the BMC LAN configuration of the managed system
- Updates the BMC LAN configuration
- Sets the BMC user password
- Gets the BMC KCS privilege of the managed system
- Sets the KCS privilege
- Loads the default factory BMC configuration
- Sets the BMC reset delay by minute
- Gets/sets the BMC user list
- Executes BMC user related actions
- Gets/deletes the Redfish Host Interface login bootstrapping account
- Sets the RMCP status of the managed system
- Gets the BMC IPMI session information of the managed system
- Gets/sets the BMC host name
- Gets/sets the USB connection for Redfish Host Interface communication
- Sets the WatchDog timer
- Executes commands to manage SNMP
- Manages a BMC IPv6 static route

### System Event Log

- Gets the event log of the managed system
- Clears the event log of the managed system
- Gets the maintenance event log of the managed system
- Clears the maintenance event log of the managed system
- Gets the crash dump of the managed system (the crash dump file is compressed)
- Sets the managed system SEL time

### CMM Management

- Updates the CMM with the given image file
- Gets the CMM information of the managed system/input CMM image file
- Gets the CMM configuration of the managed system
- Updates the CMM configuration
- Sets the CMM user password
- Loads the default factory CMM configuration
- Gets the BBP information of the managed system/input BBP image file
- Updates the BBP with the given image file
- Gets the current power status of the blade system
- Controls the power status of the CMM system
- Manages the profiles of the CMM and blade configuration on CMM
- Gets the switch information of the managed system/input switch image file
- Updates switch firmware
- Reboots the switch
- Manages the power supply unit of a managed blade system through CMM
- Gets/sets the CMM user list

### Storage Management

- Gets the RAID controller information of the managed system/input RAID image file
- Updates the RAID controller
- Gets the RAID configuration of the managed system
- Updates the RAID configuration
- Gets the SATA HDD information from the on-board AHCI controller on the managed system
- Gets the NVMe SSD information of the managed system
- Gets the PMem information of the managed system/input PMem image file
- Updates PMem firmware
- Gets the VROC configuration of the managed system
- Updates the VROC configuration
- Locates, inserts, or removes an NVMe SSD drive
- Gets the NVMe smart data of the managed system
- Gets the SAS Expander information of the managed system
- Updates the SAS Expander

### Power Management

- Prints the PSU information on the managed system
- Updates the PSU module with the OEM requested signed firmware image
- Gets the current power status of the managed system
- Sets the power action of the managed system
- Manages the system by Data Center Manageability Interface (DCMI)
- Manages the power policy of the managed system
- Gets ACPI (Advanced Configuration and Power Interface) status of the managed system
- Gets the AIOM standby power configuration of the managed system
- Sets the AIOM standby power configuration of the managed system
- Gets/sets the CPU power limit value of the managed system

### PCIe-Switch Management

- Gets the PCIe Switch information of the managed system/input PCIe Switch image file
- Updates PCIe switch firmware

### Applications

- Sends IPMI raw command
- Shows current USB access mode
- Sets current USB access mode
- Manages KMS server network configurations
- Calls Redfish API directly
- Executes shell commands on a remote system
- Executes SOL related commands
- Finds and displays all BMC devices
- Enters SAA shell mode
- Manages the BMC connection configuration in SAA shell mode

### GPU Management

- Gets the GPU information of the managed system
- Updates Delta/Delta-Next/PVC/Gaudi 2/Gaudi 3/CG1 MGX/MI300X GPU firmware
- Diagnoses the AMD MI250 GPU status of the managed system
- Gets the GPU log of the managed system
- Gets/sets the GPU power limit value of the managed system

### CPLD Management

- Gets the CPLD information of the managed system/input CPLD image file
- Updates CPLD
- Gets the Switchboard CPLD information of the managed system
- Updates the Switchboard CPLD based on the selected type
- Gets the backplane CPLD information of the managed system
- Updates the backplane CPLD
- Gets the Fanboard CPLD information of the managed system
- Updates the Fanboard CPLD based on the selected type
- Gets the AIP (AI Processor) CPLD information of the managed system
- Updates the CPLD of the AIP (AI Processor)
- Gets the AOM CPLD information of the managed system
- Updates the CPLD of the AOM
- Gets the miscellaneous CPLD information of the managed system
- Updates the miscellaneous CPLD
- Gets the Midplane SBB CPLD information of the managed system
- Updates the Midplane SBB CPLD
- Gets the NIC CPLD information of the managed system
- Updates the NIC CPLD
- Gets the Transitionboard CPLD information of the managed system
- Updates the Transitionboard CPLD

### NIC Management

- Gets the AOC NIC information of the managed system/input AOC_NIC image file
- Updates AOC NIC firmware

### Multi-Node Management

- Gets the TwinPro information of the managed system
- Updates the TwinPro configuration
- Gets the multi-node EC information of the managed system/input multi-node EC image file
- Updates the multi-node EC
- Gets the multi-node LCMC information of the managed system
- Updates the multi-node LCMC

### VM Management

- Mounts an ISO image from the image file server
- Unmounts the ISO image resources
- Mounts a floppy image from the given file
- Unmounts the floppy image file of the managed system
- Gets the virtual media information of the managed system
- Manages the virtual media devices of the managed system

### NM Management

- Manages the Intel Management Engine of the managed system
- Manages the Intel Node Manager of the managed system
- Manages the CPU of the managed system
- Manages the Compute Usage Per Second (CUPS) of the managed system

### Security Management

- Executes RoT-related actions
- Sets Secure Boot
- Gets the system lockdown status
- Sets the system lockdown mode
- Attests the managed system and manages measurements
- Securely erases RAID HDDs in a RAID storage system
- Securely erases hard disks for the managed system
- Launches the trusted platform module provision procedure
- Gets the TPM information of the managed system
- Manages the trusted platform module of the managed system
- Gets the CPU ERoT information of the managed system
- Updates CPU ERoT
- Gets the SPDM information of the managed system

### FPGA Management

- Gets the motherboard FPGA information of the managed system
- Updates the FPGA of the motherboard

### MCU Management

- Gets the motherboard MCU information of the managed system
- Updates the MCU of the motherboard

## Operations Requirements

### OOB Usage Requirements (Remote Management Server)

To run remote update operations, the managing system must meet the following requirements:

**Hardware**

- 50 MB free disk space
- 128 MB available RAM
- Ethernet network interface card

**Operating System**

- Linux: Red Hat Enterprise Linux 5.11 (x86_64) or later
- Linux: CentOS 5.11 (x86_64) or later
- Linux: Ubuntu 12.04 LTS (x86_64) or later
- Linux: Debian 7 (x86_64) or later
- Linux: SUSE Linux Enterprise Server 12 SP3 or later
- Linux: Red Hat Enterprise Linux 9.0 (aarch64) or later
- Linux: Oracle Linux 9.0 (aarch64) or later
- Linux: Rocky Linux 9.0 (aarch64) or later
- Linux: Debian 11.1.0 (aarch64) or later
- Linux: Ubuntu Server 20.04.3 (aarch64) or later
- Windows: Windows Server 2008 (x64) or later
- FreeBSD: FreeBSD 12 (x86_64) or later
- ESXi: ESXi 7.0 and ESXi 8.0

### OOB Usage Requirements (Network)

| Command | Network Requirements |
| --- | --- |
| All OOB commands | RMCP+ protocol through IPv4/IPv6 UDP with port 623 |
| `UpdateBios`, `UpdateBmc`, `UpdateCmm`, `UpdateRaidController` | In addition to RMCP+ over UDP port 623, HTTP or HTTPS through IPv4/IPv6 on the port defined in the BMC/CMM configuration is required. Default HTTP/HTTPS ports are 80 and 443, respectively |

### OOB Usage Requirements (Managed Systems)

SAA can remotely manage selected Supermicro motherboards/systems. Before use, the node product key for the managed systems must be activated — see [Licensing Managed Systems](licensing.md). Both the BMC and BIOS firmware images must also meet the following requirements.

**Firmware Image Requirements**

| Component | Requirement |
| --- | --- |
| BMC Version | X12 ATEN platform (SMT_X12): 1.00 or later; H12 ATEN platform (SMT_H12): 1.00 or later; R12 OpenBMC platform: 2.9.1-v27 or later |
| CMM Version | ATEN platform (SMT_MBIPMI): 2.45 or later |
| BIOS Version | Version 1.0 or later for select X12 3rd Generation Intel Xeon Scalable processors with Intel C620 Series Chipsets Product Family X12/H12 or later systems; Version 1.0d or later for Ampere Altra/Altra Max processor family on R12 platforms |

The `TpmProvision` command requires TPM ISO files:

| Program/Script | Description |
| --- | --- |
| `TPM_1x.3x_20170802yyyymmdd.zip` / `EFI/TPM_LOCK.ISO` | Image for TPM provision |
| `ReleaseNote.txt` | Release note for TPM ISO image usage |
| `TPM_Detect.ISO` | Image for detecting platform and TPM version |

The `CheckSystemUtilization` and `TasManage` commands require additional packages to be installed on the managed system:

| Program/Script | Description | Privilege Requirement |
| --- | --- | --- |
| `TAS_x.x.x_build.yymmdd.zip` | A Thin Agent Service (TAS) program installed on the managed system. Collects utilization information and reports it to the BMC | Root privilege of the OS running on the managed system |

The following BMC firmware is a prerequisite for TAS to run successfully:

| Component | Requirement |
| --- | --- |
| BMC Version | X12 ATEN platform (SMT_X12): 1.00 or later; H12 ATEN platform (SMT_H12): 1.00 or later |

### In-Band Usage Requirements

With in-band usage, SAA can perform BIOS/BMC/SCP/EventLog management functions for selected Supermicro motherboards/systems. The managed system must meet the following requirements.

**Hardware**

- 50 MB free disk space
- 128 MB available RAM

**Firmware Image**

- BIOS Version 1.0 or later for X12/H12 select systems
- BIOS Version 1.0d or later for Ampere Altra/Altra Max processor family on R12 platforms

**Operating System**

- Linux: Red Hat Enterprise Linux 5.11 (x86_64) or later
- Linux: CentOS 5.11 (x86_64) or later
- Linux: Ubuntu 12.04 LTS (x86_64) or later
- Linux: Debian 7 (x86_64) or later
- Linux: SUSE Linux Enterprise Server 12 SP3 or later
- Linux: Red Hat Enterprise Linux 9.0 (aarch64) or later
- Linux: Oracle Linux 9.0 (aarch64) or later
- Linux: Rocky Linux 9.0 (aarch64) or later
- Linux: Debian 11.1.0 (aarch64) or later
- Linux: Ubuntu Server 20.04.3 (aarch64) or later
- Windows: From Windows Server 2008 R2 SP1 (x64) to Windows Server 2019
- FreeBSD: FreeBSD 12 (x86_64) or later
- ESXi: ESXi 7.0 and ESXi 8.0

**Protocol and Port Requirements**

| Command | Network Requirements |
| --- | --- |
| In-Band commands through BIOS SMI or IPMI KCS | No external protocol required |
| In-Band commands through Redfish Host Interface | HTTPS through 169.254.3.254 using TCP port 443 |

**Execution Privilege Requirements**

To execute in-band functions, SAA needs root/Administrator privilege of the operating system running on the managed system.

!!! note
    Though SAA can be run on Red Hat Enterprise Linux Server 4 update 3 or later, some OSes may not be supported by the hardware. Check the OS support list for the full list of supported operating systems.

The following software should be obtained in advance:

| OS | Program/Script | Description |
| --- | --- | --- |
| Linux/Windows/FreeBSD | SAA | The main SAA program |
| Windows | `driver/phymem.sys`, `driver/pmdll64.dll` | Access physical memory and IO ports |
| ESXi | `ESXi-phymem-driver` | Access physical memory and IO ports |

Contact Supermicro for any necessary drivers.

### Additional In-Band Usage Requirements

For in-band commands (except `GetBiosInfo` and `UpdateBios`), the managed system must have a BMC firmware image and an IPMI driver installed. The BMC firmware image should meet the following requirement:

| Component | Requirement |
| --- | --- |
| BMC Version | X12 ATEN platform (SMT_X12): 1.00 or later; H12 ATEN platform (SMT_H12): 1.00 or later; R12 OpenBMC platform: 2.9.1-v27 or later |

!!! note
    For Windows Server 2008 R2 and Windows 7, the Windows driver requires Windows patch #3033929.

The following drivers should be obtained in advance:

| OS | Program/Script | Description |
| --- | --- | --- |
| Red Hat Enterprise Linux Server 4u3 or later (x86_64) / Ubuntu 12.04 or later (x86_64) / FreeBSD 12 or later (x86_64) | Built-in IPMI driver | Sends/receives data to/from BMC |

If the Linux/FreeBSD OS does not have a built-in IPMI driver, install the following:

| Program/Script | Description |
| --- | --- |
| `OpenIPMI.x86_64` | IPMI driver for accessing the BMC through its KCS interface |

### Remote In-Band Usage Requirements (Remote Management Server)

To run remote in-band operations, the managing system must meet the following requirements:

**Hardware**

- 50 MB free disk space
- 128 MB available RAM
- Ethernet network interface card

**Operating System**

- Linux: Red Hat Enterprise Linux 5.11 (x86_64) or later
- Linux: CentOS 5.11 (x86_64) or later
- Linux: Ubuntu 12.04 LTS (x86_64) or later
- Linux: Debian 7 (x86_64) or later
- Linux: SUSE Linux Enterprise Server 12 SP3 or later
- Linux: Red Hat Enterprise Linux 9.0 (aarch64) or later
- Linux: Oracle Linux 9.0 (aarch64) or later
- Linux: Rocky Linux 9.0 (aarch64) or later
- Linux: Debian 11.1.0 (aarch64) or later
- Linux: Ubuntu Server 20.04.3 (aarch64) or later
- Windows: Windows Server 2008 (x64) or later
- FreeBSD: FreeBSD 12 (x86_64) or later
- ESXi: ESXi 7.0 and ESXi 8.0

### Remote In-Band Usage Requirements (Network)

| Command | Network Requirements |
| --- | --- |
| All Remote In-Band commands | SSH protocol through IPv4 TCP port 22; SFTP protocol through IPv4 TCP port 22 |

### Remote In-Band Usage Requirements (Managed Systems)

With remote in-band, SAA can perform BIOS/BMC management functions for selected Supermicro motherboards/systems. The managed system must meet the requirements outlined in [In-Band Usage Requirements](#in-band-usage-requirements) and [Additional In-Band Usage Requirements](#additional-in-band-usage-requirements) above.

## Typographical Conventions

This manual uses the following typographical conventions.

| Convention | Definition |
| --- | --- |
| **Bold** | Keywords needing attention are in bold |
| *Italics* | Variables and section names are in italics |
| `{ }` | Curly braces indicate that at least one of the enclosed items is required |
| `[ ]` | Square brackets indicate that the enclosed item or items are optional |
| `< >` | Angle brackets enclose the parameters in the syntax description |
| `\|` | A vertical bar separates the items in a list |
| Courier New font, size 10 | Represents CLI instructions in Linux terminal mode |
| `[shell]#` | Represents the input prompt in Linux terminal mode |
| `[SAA_HOME]#` | Represents the SAA home directory prompt in Linux terminal mode |

**Obligatory choices** — curly braces and vertical bars mean choose only one option:

```
{ --enable | --disable }
```

**Optional choices** — one item in square brackets means you can choose it or omit it:

```
[ --overwrite ]
```

Square brackets and vertical bars mean choose none or only one:

```
[ --load_unique_password | --load_default_password ]
```
