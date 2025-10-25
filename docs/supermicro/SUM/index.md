# Supermicro Update Manager (SUM)

## Overview

The Supermicro Update Manager (SUM) can be used to manage the BIOS, BMC/CMM and RAID, SCP firmware image update and configuration update for select Supermicro systems. In addition, system checks as well as event log management are also supported. Moreover, special applications are also provided to facilitate system management. To update configurations, you can edit system BIOS settings, DMI information, BMC/CMM configurations and RAID configurations from readable text files, as well as use this update manager to apply these configurations.

Two channels are possible for management: the OOB (Out-Of-Band) channel, i.e., communication through the IPMI interface, and the in-band channel, i.e., communication through the local system interfaces. By the OOB channel, most management commands (except the command "CheckSystemUtilization") can be executed independently of the OS on the managed system and even before the system OS is installed.

## Features

- Command-line interfaced (CLI) and scriptable
- Independent from OS on managed systems (for OOB usage)
- Operates through OOB (Out-Of-Band) and in-band methods
- Supports concurrent execution of OOB commands on multiple systems through a system list file

### System Checks
- Checks asset device information/health remotely
- Checks if both BIOS and BMC firmware images support OOB functions
- Checks system utilization remotely
- Checks sensor data remotely
- Sends notification of system status via e-mail

### Key Management
- Activates node product keys
- Queries node product keys

### BIOS Management
- Pre-checks system board ID to prevent flashing the wrong BIOS firmware image
- Supports readable text files of BIOS configuration in plain text or XML format
- Supports readable DMI information text file to be edited
- Updates basic input/output system (BIOS) ROM
- Jumperless update of ME Flash Descriptor (FDT) region when locally update BIOS ROM
- Updates BIOS configurations (settings)
- Updates BIOS Administrator password
- Updates DMI information
- Supports Root-of-Trust (RoT) Management
- Erases OA key of the managed system
- Retrieves the BIOS firmware information of the managed system
- Updates the System Control Processor (SCP) firmware image
- Retrieves the System Control Processor (SCP) firmware information of the managed system

### BMC Management
- Supports readable text files of BMC configuration in XML format
- Updates BMC firmware image
- Updates BMC configuration
- Updates BMC password
- Sets system lockdown mode
- Sets KCS privilege levels (remotely only)
- Supports Root-of-Trust (RoT) Management

### System Event Log
- Retrieves and clears BMC and BIOS event logs
- Retrieves and clears maintenance event logs
- Downloads the system crash dump status from BMC

### Remote CMM Management
- Supports readable text file of CMM configuration in XML format
- Updates CMM firmware image
- Updates CMM configuration
- Updates CMM password
- Updates BBP firmware image
- Controls the power status of CMM system

### Storage Management
- Retrieves RAID image information from local firmware image or remote RAID controller
- Updates RAID controller firmware image remotely
- Supports the readable text files of RAID configuration in XML format
- Updates RAID configuration remotely only
- Retrieves SATA HDD information remotely only
- Retrieves NVMe information remotely only
- Securely erases an HDD on the managed system
- Securely erases hard disks (HDD or SSD) in the LSI MegaRaid SAS 3108 RAID controller system
- Updates the PMem with the given PMem file
- Retrieves the PMem firmware image information from the local or remote firmware image file
- Supports the readable text files of VROC configuration in XML format
- Updates VROC configuration.

### Applications
- Provisions/clears the trusted platform module (TPM) (remotely only)
- Gets Power status and sets power action
- Updates PSU (Power Supply Unit) firmware images and gets PSU information from the system
- Gets Graphics Processing Unit (GPU) status
- Mounts/unmounts an ISO image file from SAMBA/HTTP-shared folder (remotely only)
- Mounts/unmounts a floppy image file from a local drive
- Supports IPMI raw commands
- Supports USB Port accessibility control
- Boots into an ISO image from the image file server
- Controls the UID (User Identification) of the managed system
- Invokes Redfish API

### CPLD Management
- Updates CPLD firmware images
- Gets the AOM CPLD information from the managed system.
- Updates CPLD of AOM.
- Gets the Miscellaneous CPLD information from the managed system.
- Updates Miscellaneous CPLD.

### AIP Management
- Only retrieves the AIP CPLD information remotely
- Updates AIP CPLD firmware images

### Security Management
- Gets the CPU ERoT information from the managed system.
- Updates CPU ERoT.
- Gets the GPU ERoT information from the managed system.
- Supports Root-of-Trust (RoT) Management for CPU ERoT.
- Supports Root-of-Trust (RoT) Management for FPGA.

### FPGA Management
- Gets the motherboard FPGA information from the managed system.
- Updates the FPGA of motherboard.

### MCU Management
- Gets the motherboard MCU information from the managed system.
- Updates the MCU of motherboard.

## Operations Requirements

### OOB Usage Requirements (Remote Management Server)

To run remote update operations, you must meet the following requirements:

**System Requirements:**

- Hardware: 50 MB free disk space, 128 MB available RAM, Ethernet network interface card
- Operating System: Linux (various distributions), Windows Server 2008 or later, FreeBSD 11 or later

**Software:** SUM (main program)

### OOB Usage Requirements (Network)

- All OOB commands: RMCP+ protocol through IPv4/IPv6 UDP with port 623
- OOB commands UpdateBios, UpdateBmc, UpdateCmm and UpdateRaidController: Additionally require HTTP or HTTPS protocol through IPv4/IPv6 with ports defined in BMC/CMM configuration (default 80/443)

### OOB Usage Requirements (Managed Systems)

SUM can remotely manage selected Supermicro motherboards/systems. Node product key must be activated. BMC and BIOS firmware must meet version requirements (varies by platform).

### In-Band Usage Requirements

- Supported on Linux, Windows, FreeBSD
- Requires IPMI driver installation for some commands
- Product key activation for most commands
- Additional requirements for specific platforms and features