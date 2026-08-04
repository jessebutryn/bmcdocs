# Licensing Managed Systems

Each node is licensed by a product key. To access most SAA functions, a managed system must activate its node product key. See Appendix B, "Management Interface and License Requirements," for the complete list of functions that require activation. Product key activation is not required on the management server running SAA.

The node product key is bound to the MAC address of the BMC LAN port. Two license key formats are supported:

- **JSON** — supports all types of product keys
- **Non-JSON** — includes the formats `xxxxxxxx-xxxx-xxxx-xxxx-xxxx` for `SFT-OOB-LIC`, and a 344-byte ASCII string for other node product keys

The general flow is:

1. Receive node product keys from Supermicro — see [Getting Node Product Keys from Supermicro](#getting-node-product-keys-from-supermicro).
2. Activate the systems with those keys — see [Activating Managed Systems](#activating-managed-systems).
3. Optionally, use auto-activation instead — see [Auto-Activating Managed Systems](#auto-activating-managed-systems).

## Getting Node Product Keys from Supermicro

1. Collect the BMC MAC addresses and list them in one file, e.g. `mymacs.txt`:

    ```
    003048001012
    003048001013
    003048001014
    003048001015
    ```

2. Send this file (`mymacs.txt`) to Supermicro to obtain a node product key file (`mymacs.txt.key`). The node product key file includes the MAC address and node product key.

    Non-JSON format:

    ```
    003048001012;1111-1111-1111-1111-1111-1111-1111
    003048001013;2222-2222-2222-2222-2222-2222-2222
    003048001014;3333-3333-3333-3333-3333-3333-3333
    ```

    JSON format:

    ```
    003048001015;{"ProductKey":{"Node":{"LicenseID":"1","LicenseName":"SFT-OOBLIC","CreateDate":"20200409"},"Signature":"111111111111111111112222222222222233333333333333ababababababababababababbabcdcdcdcdcdcdccdcdcddcdefefefefefefefeefefefghghghghghghghghghghgh"}}
    ```

## Activating Managed Systems

Systems are activated using the `ActivateProductKey` command, individually or across multiple systems at once. See [ActivateProductKey](license/activateproductkey.md) for full syntax, options, and examples.

!!! note
    A node product key in JSON format must be enclosed in single quotation marks. When activating a JSON-format key on Windows, the JSON key string cannot contain any spaces.

## Auto-Activating Managed Systems

For a new, completely assembled system, its node product key can be activated during production. This is the strongly recommended method — contact a Supermicro sales representative for details.

In some cases, it is also possible to activate node product keys without running `ActivateProductKey`:

1. Collect the BMC MAC addresses of managed systems and list them in a text file, e.g. `mymacs.txt`.
2. Send this file to Supermicro through a Supermicro sales representative to obtain a credential file (`cred.bin`).
3. Put the credential file in the `SAA_HOME/credential` directory on the system where the required SAA command is run.
4. SAA will auto-activate product keys from `cred.bin` after license-required commands are run on the managed systems.

!!! note
    Auto-activation is not a site license.
