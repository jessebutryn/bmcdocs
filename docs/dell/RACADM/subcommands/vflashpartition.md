# vflashpartition

## Description

Manages the partitions on the vFlash SD card.

NOTE:

- To run this subcommand, you must have the iDRAC Enterprise license.
- After iDRAC restart, the status of the previous operation performed on the partition(s) is erased.

## Synopsis

```
racadm vflashpartition <create | delete | status | list> -i<index>
-o<label> -e<emulation type> -s<size> -f<format type> -t<partition type>
-l<path> -u<user> -p<password> -a
```

## Input

- `-o` — Label that is displayed when the partition is mounted on the operating system. This option must be a string of up to six alphanumeric characters. VFLASH is the only accepted volume label for non-Dell SD card.
- `-e` — Emulation type must be either floppy, cddvd, or hdd.
  - floppy — emulates a floppy disk
  - cddvd — emulates a CD or DVD
  - hdd — emulates a hard disk
- `-s` — Partition size in MB.
- `-f` — Format type for the partition based on the type of the file system. Valid options are raw, ext2, ext3, fat16, and fat32.
- `-t` — Create a partition of the following type:
  - empty — Creates an empty partition
  - image — Creates a partition using an image relative to iDRAC.
    Creation of a partition may be unsuccessful if:
    - The network share is not reachable.
    - The user name or password provided is not correct.
    - The file provided does not exist.
    - The memory available on the SD card is lesser than size of the image file.
- `-l` — Specifies the remote path relative to iDRAC.
- `-u` — User name for accessing the remote image.
- `-p` — Password for accessing the remote image.
- `-a` — Display the status of operations on all the existing partitions.
- `list` — Lists the existing partitions and its properties.

## Output/Example

Create a 20MB empty partition.

```
racadm vflashpartition create -i 1 -o Drive1 -e hdd -t empty -f fat16 -s 20
```

Create a partition from a remote image.

```
racadm vflashpartition create -i 1 -o Drive1 -e cddvd -t image -l //ipaddress/sharefolder/isoimge.iso -u username -p xxx
```

A new partition is created. By default, the created partition is read-only. This command is case-sensitive for the image filename extension. If the filename extension is in uppercase, for example FOO.ISO instead of FOO.iso, then the command returns a syntax error.

NOTE:

- This feature is not supported in Local RACADM.
- Creating vFlash partition from an image file on the CFS or NFS IPv6 enabled network share is not supported.

Delete a partition.

```
racadm vflashpartition delete -i 1
```

Status of operation on partition 1.

```
racadm vflashpartition status -i 1
```

Status of all the existing partitions.

```
racadm vflashpartition status -a
```

List all the existing partitions and its properties.

```
racadm vflashpartition list
```