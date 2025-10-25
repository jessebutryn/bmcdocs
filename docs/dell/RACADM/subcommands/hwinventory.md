# hwinventory

## Description

Allows you to display or export current internal hardware inventory or shipped hardware inventory by device.

NOTE: iDRAC supports a maximum of 12 parallel sessions of hardware inventory.

## Synopsis

```bash
racadm hwinventory
racadm hwinventory networktransceiver
racadm hwinventory NIC|FC|Infiniband
racadm hwinventory <FQDD>
racadm hwinventory export -f <filename> -u <username> -p <password> -l <CIFS, NFS, HTTP, or HTTPS share>
```

## Input

- `<FQDD>` — Specifies the FQDD of the target device.
  - FQDD — NIC.Slot.1–2
  - NOTE: The hwinventory subcommand supports NIC, Infiniband and FC FQDDs only.
- `-f` — Exported Hardware Inventory filename.
- `-u` — Username of the remote share to where the file must be exported. Specify user name in a domain as domain/username
- `-p` — Password for the remote share to where the file must be exported.
- `-l` — Network share location to where the Hardware Inventory must be exported.

## Examples

- To get the hwinventory, run the following command:
  ```bash
  racadm hwinventory
  ```
  Output includes detailed hardware inventory for all devices.

- To get the list of NIC FQDDs:
  ```bash
  racadm hwinventory nic
  ```

- To get the list of Infiniband FQDDs:
  ```bash
  racadm hwinventory InfiniBand
  ```

- To display the statistics for the NIC FQDD:
  ```bash
  racadm hwinventory <NIC FQDD>
  ```

- To get the complete details for a specific NIC:
  ```bash
  racadm hwinventory NIC.Integrated.1-1-1
  ```

- To get the list of network transceivers:
  ```bash
  racadm hwinventory networktransceiver
  ```

- To display the network transceiver properties with FQDD:
  ```bash
  racadm hwinventory networktransceiver NIC.Slot.1-2-1
  ```

- To export the inventory to a remote CIFS share:
  ```bash
  racadm hwinventory export -f Myinventory.xml -u admin -p xxx -l //1.2.3.4/share
  ```

- To export the inventory to a remote NFS share:
  ```bash
  racadm hwinventory export -f Myinventory.xml -u admin -p xxx -l 1.2.3.4:/share
  ```

- To export the inventory to local file system using local Racadm:
  ```bash
  racadm hwinventory export -f Myinventory.xml
  ```

- To export the inventory to a remote HTTP share:
  ```bash
  racadm hwinventory export -f Myinventory.xml -u httpuser -p httppass -l http://test.com/share
  ```

- To export the inventory to a remote HTTPS share:
  ```bash
  racadm hwinventory export -f Myinventory.xml -u httpuser -p httppass -l https://test.com/share
  ```