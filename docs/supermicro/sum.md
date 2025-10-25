# Supermicro SUM

## Overview

Supermicro Update Manager (SUM) is a tool for updating firmware and BIOS on Supermicro servers.

## Installation

Download SUM from Supermicro's website and extract the archive.

## Usage

### Update BIOS

```bash
./sum -c UpdateBios --file <bios_file> --reboot
```

### Update BMC Firmware

```bash
./sum -c UpdateBmc --file <bmc_file> --reboot
```

## Features

- BIOS updates
- BMC firmware updates
- IPMI configuration
- Hardware inventory