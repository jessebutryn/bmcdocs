# Installation and Setup

## Installing SAA

### Linux, Windows, and FreeBSD

To install SAA on Linux/FreeBSD, follow these steps. Windows installation and usage is similar.

1. Extract the `saa_x.x.x_Linux_x86_64_YYYYMMDD.tar.gz` archive file.
2. Go to the extracted `saa_x.x.x_Linux_x86_64` directory. Name this directory `SAA_HOME`.
3. Run SAA in the `SAA_HOME` directory.

Linux example:

```bash
[shell]# tar xzf saa_x.x.x_Linux_x64_YYYYMMDD.tar.gz
[shell]# cd saa_x.x.x_Linux_x86_64
[SAA_HOME]# ./saa
```

### VMware ESXi

To install the SAA user world tool and driver on ESXi, follow these steps.

1. Copy the component bundle to the ESXi server. It can be placed anywhere accessible to the ESXi console shell — these instructions assume `/tmp`.

    ```bash
    scp SMC-ESXi-saa-uw_x.x.x-0.x00.000x_xxxxxxxx.zip root@10.10.10.10:/tmp
    ```

    !!! note
        It is recommended that the SAA tool be used with the SAA release package, since binary files are required for certain commands.

2. Apply the component (the full path to the file must be specified):

    ```bash
    esxcli software component apply -d /tmp/SMC-ESXi-saa-uw_x.x.x-0.x00.000x_xxxxxxxx.zip
    ```

    After installing the component, reboot the system.

    !!! note
        If using the unsigned version of SAA, add `--no-sig-check` when installing the component:
        ```bash
        esxcli software component apply -d /tmp/SMC-ESXi-saa-uw_x.x.x-0.x00.000x_xxxxxxxx.zip --no-sig-check
        ```

3. scp the ESXi driver to the datastore:

    ```bash
    scp SMC-ESXi-phymem-driver_x.x.x-0.x00.000x_xxxxxxxx-package.zip root@10.10.10.10:/vmfs/volumes/datastore1
    ```

4. Set the `ESXi_driver` variable in `.saarc`:

    ```
    ESXi_driver = /vmfs/volumes/datastore1/SMC-ESXi-phymem-driver_x.x.x-0.x00.000x_xxxxxxxx-package.zip
    ```

5. The ESXi firewall is enabled by default — set up the whitelist. See [Installing Redfish Host Interface](#installing-redfish-host-interface) step 1 below; if the managed system does not support Redfish Host Interface, the `sh /opt/supermicro/bin/network.sh` line does not need to be added to `/etc/rc.local.d/local.sh`.

!!! note
    The `/vmfs/volumes/datastoreX` folder path may differ on your ESXi system — verify it first.

#### Installing Redfish Host Interface

The `network.sh` and `custom_service.xml` files are included in the component package. Follow these steps to set up network configuration and reboot the system afterward.

1. Add the following commands to `/etc/rc.local.d/local.sh` in the ESXi system:

    ```bash
    cp /opt/supermicro/bin/custom_service.xml /etc/vmware/firewall/
    esxcli network firewall refresh
    sh /opt/supermicro/bin/network.sh
    ```

2. Reboot the system.

`custom_service.xml` is required for the ESXi system to add the necessary ports to the firewall whitelist.

## Setting Up OOB Managed Systems

To set up OOB managed systems, follow these steps:

1. Connect the BMC/CMM to the LAN.
2. Update the BMC/CMM firmware image on the managed systems to support OOB functions, if the current version does not support it. The SAA `UpdateBmc`/`UpdateCmm` command can flash the BMC/CMM firmware image even when BMC/CMM does not currently support OOB functions.
3. Flash the BIOS ROM on the managed systems to support OOB functions, if the current version does not support it. The SAA `UpdateBios` command (either in-band or OOB) can flash BIOS even when BIOS does not currently support OOB functions. However, when using an OOB channel, if the onboard BIOS or the BIOS firmware image does not support OOB functions, DMI information (such as the MB serial number) might be lost after a system reboot.
4. Install the TAS package on the OS of the managed system (required only for the `CheckSystemUtilization` and `TasManage` commands).

!!! note
    X13 and later platforms may have a Redfish Host Interface problem. Set the `hostinterface_enable` variable in the `.saarc` file — see [Customizing SAA Configurations](basic-usage.md#customizing-saa-configurations).

### Installing the TAS Package

The TAS package (`TAS_version_build.date.zip`) can be acquired from Supermicro. Windows, Linux, FreeBSD, and ESXi platforms are supported. Refer to the TAS user guide to install it.

## Setting Up In-Band Managed Systems

For Windows OS, no action is required. If the currently installed Windows driver is old, SAA will stop TAS/SD5, load a new driver, and restart TAS/SD5. For Linux OS, no action is required either, unless the BIOS "Secure Boot" item is enabled — in that case, the Linux driver must be built and then signed.

### Building a Linux Driver

Install `kernel-devel` for the OS, then run `make` under the `SAA_HOME/driver/Source/Linux` directory.

```bash
[shell]# make
```

### Signing a Driver in Linux

After making arrangements for signing the driver (see Appendix H, "How to Sign a Driver in Linux," and obtain the keys), run:

```bash
[shell]# /lib/modules/$(uname -r)/build/scripts/sign-file sha256 <private key name>.priv <public key name>.der supermicro_phymem.ko
```

For kernels prior to 4.3.3, run the command with perl:

```bash
[shell]# perl /lib/modules/$(uname -r)/build/scripts/sign-file sha256 <private key name>.priv <public key name>.der supermicro_phymem.ko
```

## Setting Up Remote In-Band Managed Systems

Remote In-Band management sends commands via SSH and transfers files via SFTP to remote managed systems.

To set up Remote In-Band managed systems, follow these steps:

1. **Install and Start OpenSSH Server** — ensure the OpenSSH server service is installed and running on the managed systems. This is critical for enabling secure command execution and file transfers.
2. **Configure Firewall Settings** — configure the firewall on the managed systems to allow SSH access, so the systems can receive and respond to SSH commands and SFTP file transfers.
3. **Verify Installation and Configuration** — check that the OpenSSH server is operational by testing an SSH connection to the managed system:

    ```bash
    [shell]# ssh <username>@<IP or hostname>
    ```

For more detail on OpenSSH, see the OpenSSH official website.

!!! note
    To generate the keys used to sign a driver, run step 5 in Appendix H, "How to Sign a Driver in Linux": `<private key name>.priv` is the generated private key file, and `<private key name>.der` is the generated public key file.

## Setting Up VROC

Intel Virtual RAID on CPU (Intel VROC) is a hybrid RAID solution that connects NVMe SSDs directly to the PCIe lanes of Intel Xeon processors, eliminating the need for a RAID host bus adapter (HBA) and improving system performance. To use VROC with SAA, follow these steps:

1. **Install VROC Key** — Intel VROC requires a VROC key to be installed on the motherboard. The features supported depend on the type of key used.
2. **Install VROC Driver** — the VROC Redfish API requires the VROC driver to be installed. To use VROC with SAA, the VROC driver must be installed.

For more details, refer to Supermicro's official page and Intel's official page.

!!! note
    Make sure Remote In-Band managed systems meet the requirements in [In-Band Usage Requirements](overview.md#in-band-usage-requirements).

!!! note
    To use VROC with SAA, enter the operating system and wait until VROC is fully initialized.
