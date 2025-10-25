# vflashsd

## Description

Manages the vFlash SD card.

NOTE:

- To run this subcommand, you must have the iDRAC Enterprise license.
- After iDRAC restart, the status of the previous operation performed on the SD card is erased.

## Synopsis

```
racadm vflashsd <initialize | status | export | import> -l<path> -u<user> -p<password> -f<format type> -s<size> -o<label> -e<emulation type> -t<partition type>
```

## Input

- `-l` — Specifies the remote path relative to iDRAC.
- `-u` — User name for accessing the remote image.
- `-p` — Password for accessing the remote image.
- `-f` — Format type for the partition based on the type of the file system. Valid options are raw, ext2, ext3, fat16, and fat32.
- `-s` — Partition size in MB.
- `-o` — Label that is displayed when the partition is mounted on the operating system. This option must be a string of up to six alphanumeric characters. VFLASH is the only accepted volume label for non-Dell SD card.
- `-e` — Emulation type must be either floppy, cddvd, or hdd.
  - floppy — emulates a floppy disk
  - cddvd — emulates a CD or DVD
  - hdd — emulates a hard disk
- `-t` — Create a partition of the following type:
  - empty — Creates an empty partition
  - image — Creates a partition using an image relative to iDRAC.
    Creation of a partition may be unsuccessful if:
    - The network share is not reachable.
    - The user name or password provided is not correct.
    - The file provided does not exist.
    - The memory available on the SD card is lesser than size of the image file.
- `initialize` — Initializes the vFlash SD card. This command formats the SD card and creates a single partition with the specified parameters.
- `status` — Displays the status of the operation performed on the SD card.
- `export` — Exports the vFlash SD card image to a remote share.
- `import` — Imports the vFlash SD card image from a remote share.

## Output/Example

Initialize the vFlash SD card.

```
racadm vflashsd initialize -f fat16 -s 100 -o Drive1 -e hdd -t empty
```

Status of operation on the SD card.

```
racadm vflashsd status
```

Export the vFlash SD card image to a remote share.

```
racadm vflashsd export -l //ipaddress/sharefolder/vflash.img -u username -p xxx
```

Import the vFlash SD card image from a remote share.

```
racadm vflashsd import -l //ipaddress/sharefolder/vflash.img -u username -p xxx
```

NOTE:

- This feature is not supported in Local RACADM.
- Creating vFlash partition from an image file on the CFS or NFS IPv6 enabled network share is not supported.