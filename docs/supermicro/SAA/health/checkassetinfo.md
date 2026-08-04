# CheckAssetInfo

Checks the asset information for the managed system (OOB only), including add-on devices displayed under the riser cards to which they are connected. With the `--file` option, the asset information can be saved to a log file.

## Syntax

### OOB
```
saa -i <IP or host name> -u <username> -p <password> -c CheckAssetInfo [--file <filename> [--overwrite]]
```

### Multiple Systems OOB
```
saa -l <system list file> [-u <username> -p <password>] -c CheckAssetInfo [--file <filename> [--overwrite]]
```

## Options

- `--file <file name>`: (Optional) Saves the asset information to a file.
- `--overwrite`: (Optional) Overwrites the output file.

## Examples

### OOB
```bash
[SAA_HOME]# ./saa -i 192.168.34.56 -u ADMIN -p PASSWORD -c CheckAssetInfo --file log.txt
```

### Multiple Systems OOB
```bash
[SAA_HOME]# ./saa -l SList.txt -u ADMIN -p PASSWORD -c CheckAssetInfo --file log.txt
```

`SList.txt`:
```
192.168.34.56
192.168.34.57
```

If the execution "Status" field for a managed system is SUCCESS, the asset configuration of the managed system is shown in the "Execution Message" section in the created log file.

## Output

```
System
======
 Product Name:
 Product PartModel Number:
 Version: 0123456789
 Serial Number:
 UUID: 00000000-0000-0000-0000-AC1F6B0FEA62
Baseboard
=========
 Product Name: H11DSU-iN
 Version: 0123456789
 Serial Number: 0123456789
CPU
===
 [CPU(1)]
 Processor Architecture: x86
 Manufacturer: Advanced Micro Devices, Inc.
 Version: AMD EPYC 7551 32-Core Processor
 Family: AMD Zen Processor Family
 CPU ID: 12 0f 80 00 ff fb 8b 17
 Current Speed: 2000 MHz
 Total Cores: 32
 Enabled Cores: 32
 Thread Count: 64
 TDP Watts: 0
Memory
======
 [MEM(1)] N/A
 ...
 [MEM(18)]
 Locator: P2-DIMMA2
 Memory Type:
 Manufacturer: Samsung
 Manufacturing Date (YY/WW): 16/25
 Device Type: DDR4
 Serial Number: 32AEC18B
 Part Number: M393A1G40DB0-CPB
 Data Width: 64 bits
 Bus Width: 72 bits
 Current Speed: 2133 MT/s
 Size: 8192 MB
 Error Correction: MultiBitECC
 Module Type: RDIMM
 Rank: 1
Add-on Network Interface
====================================
 [[[SXB3 (Riser)]]]
 [[Onboard]]
 [NIC(1)]
 Device Class: Network controller
 Device Subclass: Ethernet controller
 Vendor: (ID:8086)
 Subvendor: (ID:15D9)
 Device Name: (ID:1528)
 Subsystem Name: (ID:0847)
 Serial Number: OA182S021066
 Part Number: AOC-UR-i4XT
 MAC Address1: AC1F6B0FEA62
 Current Speed1: 1000Mb/s
 MAC Address2: AC1F6B0FEA63
 Current Speed2: 0Mb/s
 MAC Address3: AC1F6B0FEA64
 Current Speed3: 0Mb/s
 MAC Address4: AC1F6B0FEA65
 Current Speed4: 0Mb/s
 Slot Number: Onboard
 Slot Designation: SXB3
Add-on PCI Device
====================================
 [[[SXB3 (Riser)]]]
 [[Onboard]]
 [Device(1)]
 Device Class: Network controller
 Device Subclass: Ethernet controller
 Vendor: (ID:8086)
 Subvendor: (ID:15D9)
 Device Name: (ID:1528)
 Subsystem Name: (ID:0847)
 Slot Number: Onboard
 Slot Designation: SXB3
Onboard Network Interface
====================================
 N/A
Onboard PCI Device
====================================
 [Device(1)]
 Device Class: Display controller
 Device Subclass: VGA-compatible controller
 Vendor: (ID:1A03)
 Subvendor: (ID:15D9)
 Device Name: (ID:2000)
 Subsystem Name: (ID:0963)
 Device Status of Video1: Enabled
 Device Type: Video
 Reference Designation of Video1: ASPEED Video AST2500
 [Device(2)]
 Device Class: Serial bus controller
 Device Subclass: Universal Serial Bus(USB) Host Controller following the Intel eXtensible Host Controller Interface (xHCI) Specification
 Vendor: (ID:1B21)
 Subvendor: (ID:1B21)
 Device Name: (ID:1142)
 Subsystem Name: (ID:1142)
 Device Status of Other1: Enabled
 Device Type: Other
 Reference Designation of Other1: ASMedia USB 3.1
System Network Interface
====================================
 [LAN(1)]
 MAC Address: AC1F6B0FEA62
 IPv4 Address: 10.146.172.29
 IPv6 Address: 2001:db8:0:f102:4195:1c5:4d3:dd25,2001:db8::536c:93e5:b88f:9796,fe80::5e30:66bf:aca9:42f
 Current Speed: 1000Mb/s
 [LAN(2)]
 MAC Address: AC1F6B0FEA63
 IPv4 Address: N/A
 IPv6 Address: N/A
 Current Speed: 0Mb/s
IPMI Network Interface
====================================
 [IPMI]
 MAC Address: 0025905E9153
Power Supplies
====================================
 [(PSU1)]
 Model: PWS-2K05A-1R
 Serial Number: P2K5ACI49CT0013
 Type: AC
 Capacity Watts: 2000 W
 Firmware Version: 1.2
 Sensor Number: 196
```

Also reported (per the "SYSTEM" execution message summary):
```
[SYSTEM]
System Supports RoT Feature......Yes
```

## Notes

- Items generally supported are: System Product Name, Serial Number, System Network Interface, and IPMI Network Interface.
- Current Speed in the Network Interface section requires TAS installed on the managed system.
- For riser card chips, device information is listed in the add-on card section under the label "Onboard."
