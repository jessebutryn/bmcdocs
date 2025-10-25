# systemerase

## Description

Allows you to erase the components to remove the server from use.

## Synopsis

```
racadm systemerase <component>
racadm systemerase <component>,<component>,<component>
```

## Input

- `<component>` — The valid types of components are:
  - bios — To reset the BIOS to default.
  - diag — To erase embedded diagnostics.
  - drvpack — To erase embedded OS driver pack.
  - idrac — To reset the iDRAC to default.
  - lcdata — To erase Lifecycle Controller data.
  - allaps — To reset all apps.
  - secureerasepd — To erase the physical disk. This supports SED, NVMe drives, and PCIe cards.
  - overwritepd — To overwrite physical disk. This supports SAS and SATA drives.
  - percnvcache — To erase NV cache.
  - vflash — To erase vFlash.
  - nvdimm — To erase all NonVolatileMemory.

## Output/Example

Erase BIOS.

```
racadm systemerase bios
```

Erase diagnostics.

```
racadm systemerase diag
```

Erase driver pack.

```
racadm systemerase drvpack
```

Reset iDRAC to default.

```
racadm systemerase idrac
```

Erase Lifecycle Controller data.

```
racadm systemerase lcdata
```

Reset all apps.

```
racadm systemerase allapps
```

Secure erase physical disk.

```
racadm systemerase secureerasepd
```

Overwrite physical disk.

```
racadm systemerase overwritepd
```

Erase NV cache.

```
racadm systemerase percnvcache
```

Erase vFlash.

```
racadm systemerase vflash
```

Erase multiple components.

```
racadm systemerase bios,diag,drvpack
racadm systemerase bios,idrac,lcdata
racadm systemerase secureerasepd,vflash,percnvcache
```

Erase NVDIMM.

```
racadm systemerase nvdimm
```