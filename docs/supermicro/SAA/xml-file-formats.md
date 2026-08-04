# XML File Formats

SAA uses XML files to represent editable configuration for BIOS, BMC, CMM, RAID, VROC, TwinPro, and fixed boot settings. Each configuration domain has its own XML schema, described below. For details on modifying BIOS configuration values in an XML file, see Appendix E ("How to Change BIOS Configurations in XML Files") of the SAA User's Guide. For editing XML files from the command line, see Appendix F ("Using the Command Line Tool (XMLStarlet) to Edit XML Files").

## BIOS Settings XML File Format

The `BiosCfg.xml` file displays the BIOS setup menu in XML format for easier configuration. Each setting consists of a default value and a current value. The XML version appears on the first line.

```xml
<BiosCfg>
  <Menu name="IPMI">
    <Menu name="System Event Log">
      <Information>
        <Help><![CDATA[Press <Enter> to change the SEL event log
configuration.]]></Help>
      </Information>
      <Subtitle>Enabling/Disabling Options</Subtitle>
      <Setting name="SEL Components" selectedOption="Enabled" type="Option">
        <Information>
          <AvailableOptions>
            <Option value="0">Disabled</Option>
            <Option value="1">Enabled</Option>
          </AvailableOptions>
          <DefaultOption>Enabled</DefaultOption>
          <Help><![CDATA[Change this to enable or disable all features of System
Event Logging during boot.]]></Help>
        </Information>
      </Setting>
      <Subtitle></Subtitle>
      <Subtitle>Erasing Settings</Subtitle>
      <Setting name="Erase SEL" selectedOption="No" type="Option">
        <Information>
          <AvailableOptions>
            <Option value="0">No</Option>
            <Option value="1">Yes, On next reset</Option>
            <Option value="2">Yes, On every reset</Option>
          </AvailableOptions>
          <DefaultOption>No</DefaultOption>
          <Help><![CDATA[Choose options for erasing SEL.]]></Help>
          <WorkIf><![CDATA[ 0 != SEL Components ]]></WorkIf>
        </Information>
      </Setting>
    </Menu>
  </Menu>
</BiosCfg>
```

- The root table name is `BiosCfg`, enclosed by the `<BiosCfg>`/`</BiosCfg>` tag pair. All configuration is nested inside it.
- `<Menu>` is the only tag type that extends directly from `<BiosCfg>`. Each `<Menu>` can enclose further `<Menu>`, `<Information>`, `<Setting>`, `<Subtitle>`, and `<Text>` tags.
- `<Information>` displays `<Help>` and `<WorkIf>`, plus setting-specific data — for example, an `Option`-type `<Setting>` lists `<AvailableOptions>` and `<DefaultOption>`. Modifying anything inside `<Information>` has no effect.
- `<Setting>` is the only configurable part of the file. Five setting types are supported: `Option`, `CheckBox`, `Numeric`, `String`, and `Password`. Each type has its own set of accepted enclosures — for `Option`, the accepted `selectedOption` values are listed under `<AvailableOptions>`; any other value throws an exception.
- `<Subtitle>` and `<Text>` indicate what follows in the configuration; `<Help>` provides explanatory text for menus and settings.
- `<WorkIf>` determines whether a setting modification takes effect. If absent, the modified value always takes effect. If present and evaluated `false`, SAA warns that the change will not take effect.
- If the value in `selectedOption` is not one of the values listed in `<AvailableOptions>`, SAA throws an exception.
- Two or more settings in the file might refer to the same underlying variable in the BIOS binary (for example, "Quiet Boot" appears under both Setup → Advanced → Boot Feature and Setup → Boot as distinct settings that share the same BIN variable). If their values conflict in the XML file, SAA throws an exception.

## BMC Configuration XML File Format

The BMC configuration file displays supported and editable BMC configuration elements in XML format.

```xml
<xml version="1.0">
<BmcCfg>
  <!--You can remove unnecessary elements so that-->
  <!--their values will not be changed after update-->
  <StdCfg Action="None">
    <!--Supported Action:None/Change-->
    <!--Standard BMC configuration tables-->
    <FRU Action="Change">
      <!--Supported Action:None/Change-->
      <Configuration>
        <!--Configuration for FRU data-->
        <BoardMfgName>Supermicro</BoardMfgName>
        <!--string value, 0~16 characters-->
      </Configuration>
    </FRU>
  </StdCfg>
  <OemCfg Action="Change">
    <!--Supported Action:None/Change-->
    <!--OEM BMC configuration tables-->
    <ServiceEnabling Action="Change">
      <!--Supported Action:None/Change-->
      <Configuration>
        <!--Configuration for ServiceEnabling-->
        <HTTP>Enable</HTTP>
        <!--Enable/Disable-->
      </Configuration>
    </ServiceEnabling>
  </OemCfg>
</BmcCfg>
```

- The root table name is `BmcCfg`. The root table has up to two direct children: `StdCfg` and `OemCfg`, which can themselves have child tables.
- Configurable elements are listed in the `Configuration` field of each child table; each element has a name tag pair enclosing its value.
- Comments follow any element or table tag, enclosed by `<!--` and `-->`, and describe supported usage.
- Configuration tables can carry an `Action` attribute (supported actions are noted in the comments). If `Action="None"`, all configuration and children of that table are skipped. Tables may also carry other table-specific attributes as needed.
- In the example above, `StdCfg` has `Action="None"`, so SAA skips updating `BoardMfgName` in the `FRU` table; `OemCfg` has `Action="Change"`, so SAA tries to update `HTTP` in `ServiceEnabling` to `Enable`.

### Pure Redfish LAN Table in BMC Configuration

If the LAN version of the Redfish API is 1.6.3 or greater, SAA supports a pure Redfish LAN table in the BMC configuration. To check the LAN version, query the Redfish API endpoint `/redfish/v1/Managers/1/EthernetInterfaces/1` with `GET` and inspect the `@odata.type` field of the response — for example: `"#EthernetInterface.v1_6_3.EthernetInterface"`.

The XPaths differ between the legacy IPMI LAN table and the pure Redfish LAN table:

**General settings**

| IPMI LAN table | Pure Redfish LAN table |
|---|---|
| `/BmcCfg/OemCfg/LAN/Configuration/LanMode` | `/BmcCfg/OemCfg/LAN/Configuration/LanInterface` |
| `/BmcCfg/OemCfg/LAN/Configuration/ShareLan` | `/BmcCfg/OemCfg/LAN/Configuration/LanInterface` |
| `/BmcCfg/OemCfg/LAN/Configuration/MacAddr` | `/BmcCfg/OemCfg/LAN/Information/MacAddress` |
| `/BmcCfg/OemCfg/LAN/Configuration/VLAN_Enable` | `/BmcCfg/OemCfg/LAN/Configuration/VLANEnable` |
| `/BmcCfg/OemCfg/LAN/Configuration/VLAN_ID` | `/BmcCfg/OemCfg/LAN/Configuration/VLANId` |

**IPv4 settings**

| IPMI LAN table | Pure Redfish LAN table |
|---|---|
| `/BmcCfg/OemCfg/LAN/Configuration/IPv4/Configuration/IPSrc` | `/BmcCfg/OemCfg/LAN/Configuration/IPv4/Configuration/DHCPEnabled` |
| `/BmcCfg/OemCfg/LAN/Configuration/IPv4/Configuration/IPAddr` | `/BmcCfg/OemCfg/LAN/Configuration/IPv4/Configuration/Address` |
| `/BmcCfg/OemCfg/LAN/Configuration/IPv4/Configuration/DefaultGateWayAddr` | `/BmcCfg/OemCfg/LAN/Configuration/IPv4/Configuration/Gateway` |
| `/BmcCfg/OemCfg/LAN/Configuration/IPv4/Configuration/DNSAddr` | `/BmcCfg/OemCfg/LAN/Configuration/IPv4/Configuration/IPv4StaticNameServer1` |
| `/BmcCfg/OemCfg/LAN/Configuration/IPv4/Configuration/DNSAddr2` | `/BmcCfg/OemCfg/LAN/Configuration/IPv4/Configuration/IPv4StaticNameServer2` |

**IPv6 settings**

| IPMI LAN table | Pure Redfish LAN table |
|---|---|
| `/BmcCfg/OemCfg/LAN/Configuration/DynamicIPv6/Configuration/AutoConfiguration` | `/BmcCfg/OemCfg/LAN/Configuration/IPv6/Configuration/DynamicIPv6/Configuration/IPv6AutoConfigEnabled` |
| `/BmcCfg/OemCfg/LAN/Configuration/DynamicIPv6/Configuration/DHCPv6Mode` | `/BmcCfg/OemCfg/LAN/Configuration/IPv6/Configuration/DynamicIPv6/Configuration/OperatingMode` |
| `/BmcCfg/OemCfg/LAN/Configuration/StaticIPv6/Configuration/DNSv6Mode` | `/BmcCfg/OemCfg/LAN/Configuration/IPv6/Configuration/IPv6UseDNSServers` |
| `/BmcCfg/OemCfg/LAN/Configuration/StaticIPv6/Configuration/IPv6StaticNameServer` | `/BmcCfg/OemCfg/LAN/Configuration/IPv6/Configuration/IPv6StaticNameServer1` |

## BMC LAN Configuration XML File Format

The BMC LAN configuration file displays supported and editable BMC LAN configuration elements in XML format.

```xml
<?xml version="1.0"?>
<BmcLANCfg>
  <!--You can remove unnecessary elements so that-->
  <!--their values will not be changed after update-->
  <LAN Action="None">
    <!--Supported Action:None/Change-->
    <Information>
      <!--Information for LAN properties-->
      <SpeedMbps>1000</SpeedMbps>
      <Duplex>Full Duplex</Duplex>
    </Information>
    <Configuration>
      <!--Configuration for LAN properties-->
      <!--Will be skipped in OOB usage mode if BMC doesn't support.-->
      <IPProtocolStatus>Dual</IPProtocolStatus>
      <!--IPv4/IPv6/Dual-->
      <LanMode>Share</LanMode>
      <!--Dedicated/Share/Failover-->
      <!--Changing this setting may cause the LAN to be unavailable.-->
      <MacAddr>3C:EC:EF:C6:22:D9</MacAddr>
      <!--X:X:X:X:X:X-->
      <!--Will be skipped in OOB usage mode.-->
      <Link></Link>
      <!--Auto Negotiation/10M Half Duplex/10M Full Duplex/100M Half Duplex/100M Full Duplex-->
      <!--Link can only be updated if LanMode is Dedicated. Will be skipped if empty.-->
      <HostName></HostName>
      <!--BMC host name, string value; length limit = 63 characters-->
      <CommunityString>public</CommunityString>
      <!--string value; length limit = 18 characters-->
      <VLAN_Enable>Disable</VLAN_Enable>
      <!--Enable/Disable. Changing this setting may cause the LAN to be unavailable.-->
      <VLAN_ID>1</VLAN_ID>
      <!--Integer value is in [1-4094]. 0 and 4095 for special purposes.-->
      <!--When VLAN enabled, 0 is prohibited.-->
      <RMCP_Port>623</RMCP_Port>
      <!--[1-65535]. In OOB usage, default RMCP port is 623.-->
      <!--If updated, configure 'rmcp_port' in .saarc for OOB BMC connection.-->
      <IPv4 Action="Change">
        <!--Supported Action:None/Change-->
        <Configuration>
          <!--Configuration for IPv4 properties-->
          <IPSrc>DHCP</IPSrc>
          <!--Static/DHCP-->
          <IPAddr>192.168.34.56</IPAddr>
          <!--X.X.X.X, each field an integer in [0-255]-->
          <SubNetMask>255.255.224.0</SubNetMask>
          <DefaultGateWayAddr>10.184.7.254</DefaultGateWayAddr>
          <DNSAddr>1.1.1.1</DNSAddr>
          <!--Will be skipped if empty.-->
          <DNSAddr2>2.2.2.2</DNSAddr2>
          <!--DNSAddr2 is read-only.-->
        </Configuration>
      </IPv4>
    </Configuration>
  </LAN>
</BmcLANCfg>
```

- The root table name is `BmcLANCfg`.
- Child tables or configurable elements can be deleted to skip updating them, but a child cannot exist without its parent.
- The XML version line and root table must not be deleted.
- Configuration tables can have an `Action` attribute; `Action="None"` skips all configuration and children of that table. In the example, `LAN` has `Action="None"`, so `IPProtocolStatus`, `LanMode`, `MacAddr`, `Link`, `HostName`, `CommunityString`, `VLAN_Enable`, `VLAN_ID`, and `RMCP_Port` are all skipped, while `IPv4` has `Action="Change"` so SAA attempts to update `IPSrc`.
- Fields marked "will be skipped in multiple system usage without `--individually` option" only apply per-system when that option is used.

## CMM Configuration XML File Format

The CMM configuration file contains CMM configuration elements in XML format.

```xml
<?xml version="1.0"?>
<CmmCfg>
  <!--You can remove unnecessary elements so that-->
  <!--their values will not be changed after update-->
  <StdCfg Action="None">
    <!--Supported Action:None/Change-->
    <!--Standard Cmm configuration tables-->
    <SOL Action="Change">
      <!--Supported Action:None/Change-->
      <Configuration>
        <!--Configuration for SOL properties-->
        <Access>Enable</Access>
        <!--Enable/Disable-->
      </Configuration>
    </SOL>
  </StdCfg>
  <OemCfg Action="Change">
    <!--Supported Action:None/Change-->
    <!--OEM Cmm configuration tables-->
    <ServiceEnabling Action="Change">
      <!--Supported Action:None/Change-->
      <Configuration>
        <!--Configuration for ServiceEnabling-->
        <HTTP>Enable</HTTP>
        <!--Enable/Disable-->
      </Configuration>
    </ServiceEnabling>
  </OemCfg>
</CmmCfg>
```

- The root table name is `CmmCfg`, with up to two child tables: `StdCfg` and `OemCfg`, which can themselves have child tables.
- Configurable elements are listed in the `Configuration` field of each child table, each enclosed by a name tag pair.
- Configuration tables can carry an `Action` attribute; `Action="None"` skips all configuration and children of that table.
- Child tables or configurable elements can be deleted to skip updates, but cannot exist without their parent. The XML version line and root table must not be deleted.

## RAID Configuration XML File Format

The RAID configuration file displays editable RAID configuration elements in XML format.

- The root table name is `RAIDCfg`, with up to three children: `Information`, `BroadcomRAIDController`, and `MarvellRAIDController`, which can have their own child tables.
- Configurable elements are listed in the `Configuration` field of each child table.
- Configuration tables can carry an `Action` attribute; `Action="None"` skips all configuration and children.

**Broadcom controller (`BroadcomRAIDController` table):**

- To create a logical volume: set the `RAIDInfo` action to `Change` and the `RAID` action to `Create`. `PhysicalDriveList` must contain all drive IDs for the RAID, and `ArrayID` must be `-1`.
- To delete a logical volume: set `RAIDInfo` to `Change`, `RAID` action to `Delete`, and assign the logical drive ID (or `ALL`) to `DeletingLogicalDriveList`.
- To delete all arrays on the controller: set `RAIDInfo` action to `ClearAll`.
- To change a RAID's configuration: delete the original RAID and create a new one with `Level`, `Span`, and `PhysicalDriveList` modified as needed.
- To enable a drive's HDD LED: add the drive ID to `LocatingPhysicalDriveIDList` and set the RAID action to `Locate`.
- To disable a drive's HDD LED: add the drive ID to `UnlocatePhysicalDriveIDList` and set the RAID action to `Unlocate`.

**Marvell controller (`MarvellRAIDController` table):**

- To create a logical drive: set `RAIDInfo` to `Change`, `RAID` action to `Create`, `ArrayID` to `0`.
- To delete a logical drive: set `RAIDInfo` to `Change`, `RAID` action to `Delete`, and assign the drive ID to `LogicalDriveDeleteID`.
- To rebuild a logical drive: set `RAIDInfo` to `Change`, `RAID` action to `Rebuild`, and assign the drive ID to `LogicalDriveRebuildID`.
- To import a logical drive: set `RAIDInfo` to `Change`, `RAID` action to `Import`, and assign the drive ID to `LogicalDriveImportID`.

Supported RAID levels on the Broadcom controller: 0/1/5/6/10/50/60. Marvell controllers only support RAID 1 (up to two drives on AOC-SLG2-2TM2).

| RAID Level | Span Value | Minimum Physical HDDs |
|---|---|---|
| 0 | 1 | 1 |
| 1 | 1 | 2 |
| 5 | 1 | 3 |
| 6 | 1 | 3 |
| 10 | 2 or 4 | 4 |
| 50/60 | 3 or 4 | 6 |

The number of physical hard drives must be a multiple of the "Span" value on the Broadcom controller.

Example (Broadcom):

```xml
<?xml version="1.0"?>
<RAIDCfg>
  <Information>
    <TotalRaidController>2</TotalRaidController>
  </Information>
  <BroadcomRAIDController Action="Change" DeviceID="0" DeviceName="AVAGO 3108 MegaRAID">
    <!--Supported Action:None/Change-->
    <ControllerProperties Action="None">
      <!--Supported Action:None/Change-->
      <Configuration>
        <BiosBootMode>Stop on Error</BiosBootMode>
        <!--Supported values: Stop on Error/Pause on Error/Ignore Errors/Safe Mode on Error-->
        <JbodMode>Disable</JbodMode>
        <!--Supported values: Enable/Disable-->
      </Configuration>
    </ControllerProperties>
    <RAIDInfo Action="Change">
      <!--Supported Action:None/Change/ClearAll-->
      <RAID Action="None" ArrayID="-1">
        <!--Supported Action:None/Add/Delete/Create/Locate/Unlocate-->
        <Configuration>
          <Level>RAID0</Level>
          <!--Supported values: RAID0/RAID1/RAID5/RAID6/RAID10/RAID50/RAID60-->
          <Span>1</Span>
          <PhysicalDriveList></PhysicalDriveList>
          <NewLogicalCount>1</NewLogicalCount>
          <PercentageToUsed>100</PercentageToUsed>
          <StripSize>256KB</StripSize>
          <!--Valid: 64KB/128KB/256KB/512KB/1MB. Default: 256KB-->
          <LogicalDriveName></LogicalDriveName>
        </Configuration>
      </RAID>
    </RAIDInfo>
  </BroadcomRAIDController>
</RAIDCfg>
```

## VROC Configuration XML File Format

The VROC configuration file displays editable Intel VROC configuration elements in XML format.

```xml
<?xml version="1.0"?>
<VROCCfg>
  <PhysicalDriveInfo>
    <Information>
      <!--Physical hard drive information, this region is read only.-->
      <DriveCount>2</DriveCount>
      <PhysicalDrive VROCId="25362e54-a291-5a0f-a3e7-71ec761b4838">
        <DriveStatus>Enabled</DriveStatus>
        <Temperature>0</Temperature>
        <Capacity>2980</Capacity>
        <ModelName>INTEL SSDPE2KE032T8</ModelName>
        <SerialNumber>PHLN1175029U3P2BGN</SerialNumber>
        <CapableSpeed>0Gb/s</CapableSpeed>
        <PredictedFail>false</PredictedFail>
      </PhysicalDrive>
    </Information>
  </PhysicalDriveInfo>
  <VolumeInfo Action="Change">
    <!--Supported Action:None/Change/ClearAll-->
    <Volume Action="None" VROCId="e66e93dc-a28b-5072-8c02-ec48ecb3bccb">
      <!--Supported Action:None/Delete/Create-->
      <Information>
        <Encrypted>false</Encrypted>
        <BlockSize>512</BlockSize>
      </Information>
      <Configuration>
        <Name>TestRaid_0</Name>
        <!--Volume name, string value; length limit = 15 characters. Only for "Create".-->
        <Level>RAID1</Level>
        <!--Valid value: RAID0/RAID1/RAID5/RAID10. Only for "Create".-->
        <PhysicalDriveList></PhysicalDriveList>
        <!--Comma-separated; supports VROCId or Serial Number.-->
        <!--Valid drive count: 1~96 (any) for RAID0, 2 (even) for RAID1,-->
        <!--3~96 (any) for RAID5, 4 (even) for RAID10. Only for "Create".-->
        <StripSize>64</StripSize>
        <!--Strip size (KB). RAID0: 4/8/16/32/64/128. RAID1: 64.-->
        <!--RAID5: 4/8/16/32/64/128. RAID10: 4/8/16/32/64/128. Only for "Create".-->
        <Capacity>2899742</Capacity>
        <!--Capacity size (MB). Only for "Create".-->
      </Configuration>
    </Volume>
  </VolumeInfo>
</VROCCfg>
```

- The root table name is `VROCCfg`, with two children: `PhysicalDriveInfo` (read-only physical drive information) and `VolumeInfo` (configurable volumes).
- To create a logical volume: set `VolumeInfo` action to `Change`, `Volume` action to `Create`, `PhysicalDriveList` to all VROC IDs or serial numbers to include, and `VROCId` to `-1`.
- To delete a logical volume: set `VolumeInfo` to `Change`, `Volume` action to `Delete`, and specify the corresponding VROC ID.
- To delete all arrays: set `VolumeInfo` action to `ClearAll` (the VROC ID is then irrelevant).
- To change a VROC configuration: delete the original controller and create a new one with modified `Name`, `Level`, `PhysicalDriveList`, `StripSize`, and `Capacity`.
- Supported RAID level varies by the VROC key installed on the motherboard:

| Supermicro P/N | Description | RAID Support |
|---|---|---|
| AOCVROCINTMOD | Intel SSD Only Upgrade module | RAID 0/1/10/5 |
| AOCVROCSTNMOD | Standard Upgrade module | RAID 0/1/10 |
| AOCVROCPREMOD | Premium Upgrade module | RAID 0/1/10/5 |

For Intel PCIe Gen3 x8 SSDs, an Intel VROC hardware key is not required for RAID 0, while a key is required for RAID 0/1/5/10 on most other SSDs. See the Supermicro website for VROC key details.

## TwinPro Configuration XML File Format

The TwinPro configuration file displays supported and editable TwinPro configuration elements in XML format.

```xml
<?xml version="1.0"?>
<TwinProCfg>
  <TwinProInfo>
    <!--Twin Pro information, this region is read only.-->
    <Information>
      <MicroCloudSystem>False</MicroCloudSystem>
      <NodeA>
        <Power>Active</Power>
        <IP>172.31.54.15</IP>
        <IPv6></IPv6>
        <!--only for Micro Cloud system-->
        <Watts>262W</Watts>
        <Current>21.3A</Current>
        <CPU1Temp>33C</CPU1Temp>
        <CPU2Temp>28C</CPU2Temp>
        <SystemTemp>23C</SystemTemp>
        <NodePN></NodePN>
        <NodeSN>HM227S012083</NodeSN>
      </NodeA>
      <NodeB>
        <Power>Active</Power>
        <IP>172.31.36.228</IP>
        <Watts>294W</Watts>
        <Current>24.1A</Current>
        <CPU1Temp>31C</CPU1Temp>
        <CPU2Temp>29C</CPU2Temp>
        <SystemTemp>20C</SystemTemp>
        <NodeSN>HM227S012108</NodeSN>
      </NodeB>
    </Information>
  </TwinProInfo>
  <CurrentNodeInfo Action="Change" Node="A">
    <!--Supported Action:None/Change-->
    <!--NodeId is current node ID-->
    <Information>
      <BackPlaneRevision>1.00</BackPlaneRevision>
      <BpnId>35</BpnId>
      <TwinType>A7</TwinType>
      <MCU1Version>0.12</MCU1Version>
      <MCU2Version>0.00</MCU2Version>
    </Information>
    <Configuration>
      <ConfigId>2</ConfigId>
      <SystemName>SystemName</SystemName>
      <!--string value; length limit = 20 characters-->
      <SystemPN>SystemPN</SystemPN>
      <SystemSN>SystemSN</SystemSN>
      <ChassisPN>ChassisPN</ChassisPN>
      <ChassisSN>ChassisSN</ChassisSN>
      <BackPlanePN>BackPlanePN</BackPlanePN>
      <BackPlaneSN>BackPlaneSN</BackPlaneSN>
      <NodePN>NodePN</NodePN>
      <NodeSN>NodeSN</NodeSN>
      <ChassisLocation>00 00 00 00 00</ChassisLocation>
      <!--Hex value, 5 bytes, space separated-->
      <BackPlaneLocation>N/A</BackPlaneLocation>
      <!--FatTwin only, Valid value: Right/Left; else Hex. Skipped if N/A.-->
    </Configuration>
  </CurrentNodeInfo>
</TwinProCfg>
```

- The root table name is `TwinProCfg`, with two direct children: `TwinProInfo` (read-only node status) and `CurrentNodeInfo` (configurable, scoped to the node being configured via the `Node` attribute).
- In the example, `TwinProInfo` shows a two-node system with both nodes Active, and `CurrentNodeInfo` is configuring Node A.
- Child tables or configurable elements can be deleted to skip updates, but cannot exist without a parent.

## Fixed Boot Configuration XML File Format

The fixed boot configuration is used to power a boot device on or off and to change the boot device order on X13 and later platforms.

```xml
<?xml version="1.0" encoding="ISO-8859-1" standalone="yes"?>
<FixedBootCfg>
  <!-- SuperServer Automation Assistant 1.0.0 (2023/08/16)-->
  <!--File generated at 2023-08-17_14:30:43-->
  <!--Boot mode selected UEFI-->
  <Menu name="Fixed Boot Order">
    <Setting name="Boot Option #1" selectedOption="UEFI Hard Disk:UEFI OS" type="Option">
      <Information>
        <AvailableOptions>
          <Option>UEFI Hard Disk:UEFI OS (SATA,Port:0)</Option>
          <Option>UEFI CD/DVD</Option>
          <Option>UEFI USB Hard Disk</Option>
          <Option>UEFI USB CD/DVD</Option>
          <Option>UEFI USB Key</Option>
          <Option>UEFI USB Floppy</Option>
          <Option>UEFI USB Lan</Option>
          <Option>UEFI Network:(B4/D0/F0) UEFI PXE IPv4 Intel Ethernet Controller X550(MAC:3cecefcb33c6)</Option>
          <Option>UEFI AP:UEFI: Built-in EFI Shell</Option>
          <Option>Disabled</Option>
        </AvailableOptions>
        <DefaultOption>UEFI Hard Disk:UEFI OS (SATA,Port:0)</DefaultOption>
      </Information>
    </Setting>
    <!-- Boot Option #2 through #9 follow the same pattern -->
  </Menu>
  <Menu name="UefiHardDiskBBSPriorities">
    <Setting name="UEFIHardDisk #1" selectedOption="UEFI OS (SATA,Port:0)" type="Option">
      <Information>
        <AvailableOptions>
          <Option>UEFI OS (SATA,Port:0)</Option>
          <Option>Disabled</Option>
        </AvailableOptions>
        <DefaultOption>UEFI OS (SATA,Port:0)</DefaultOption>
      </Information>
    </Setting>
  </Menu>
  <Menu name="UefiApplicationBootPriorities">
    <Setting name="UEFIAP #1" selectedOption="UEFI: Built-in EFI Shell" type="Option">
      <Information>
        <AvailableOptions>
          <Option>UEFI: Built-in EFI Shell</Option>
          <Option>Disabled</Option>
        </AvailableOptions>
        <DefaultOption>UEFI: Built-in EFI Shell</DefaultOption>
      </Information>
    </Setting>
  </Menu>
  <Menu name="UefiNetworkBBSPriorities">
    <Setting name="UEFINetwork #1" selectedOption="(B4/D0/F1) UEFI PXE IPv4 Intel Ethernet Controller X550(MAC:3cecefcb33c7)" type="Option">
      <Information>
        <AvailableOptions>
          <Option>(B4/D0/F0) UEFI PXE IPv4 Intel Ethernet Controller X550(MAC:3cecefcb33c6)</Option>
          <Option>(B4/D0/F1) UEFI PXE IPv4 Intel Ethernet Controller X550(MAC:3cecefcb33c7)</Option>
          <Option>Disabled</Option>
        </AvailableOptions>
        <DefaultOption>(B4/D0/F0) UEFI PXE IPv4 Intel Ethernet Controller X550(MAC:3cecefcb33c6)</DefaultOption>
      </Information>
    </Setting>
  </Menu>
</FixedBootCfg>
```

- The root table name is `FixedBootCfg`. There can be several `<Menu>` tags, depending on the managed system's boot devices.
- Configurable elements are listed in the `<Setting>` field of each menu. `<Information>` (with `<AvailableOptions>` and `<DefaultOption>`) is informational only — modifying it has no effect.
- To change a setting, modify the `selectedOption` attribute of the relevant `<Setting>` tag to one of the values listed in `<AvailableOptions>`.
- After making changes, save the XML file and run `ChangeFixedBootCfg` with the `--reboot` option; the change takes effect after reboot.
- Unchanged settings can be deleted to skip the update. The XML version line and `<FixedBootCfg>` root must not be deleted.
- A boot device's on/off state is modified in the corresponding `<xxxxxBBSPriorities>` `<Setting>` menu — but if the device is currently on the boot order list, it must first be removed from the boot order before it can be disabled there.
- If more than one device is listed in an `<xxxxxBBSPriorities>` menu, changing their order there also changes the boot order shown in the "Fixed Boot Order" menu for that device class (for example, reordering the two UEFI Network devices under `UefiNetworkBBSPriorities` changes which one appears for the "UEFI Network" option in "Fixed Boot Order"). The UEFI Network display device cannot be changed directly in "Fixed Boot Order".
- `<WorkIf>` does not apply in `FixedBootCfg`, since there is no `<WorkIf>` in its `Configuration` sections.

## Notes

- The BMC, BMC LAN, and CMM configuration XML files may contain extended ASCII characters (such as (c), (r), and u). Use a text editor that supports extended ASCII (ISO-8859-1 encoding) — Notepad++ on Windows or Vim on Linux are suggested — otherwise those characters may be lost on save.
- If garbled characters appear when viewing/editing with vim, vim may be misdetecting the file encoding. Add `set fileencodings=latin1,ucs-bom,utf-8,gb18030` to `~/.vimrc`.
