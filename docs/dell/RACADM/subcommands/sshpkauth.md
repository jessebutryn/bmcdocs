# sshpkauth

## Description

Enables you to upload and manage up to 4 different SSH public keys for each user. You can upload a key file or key text, view keys, or delete keys.

This command has three mutually exclusive modes determined by the options — upload, view, and delete.

To run this subcommand, you must have Configure user privilege.

## Synopsis

```
racadm sshpkauth -i svcacct -k <key_index> -t <PK_key_text>
racadm sshpkauth -i svcacct -k <key_index> -f <PK_key_text>
racadm sshpkauth -v -i svcacct -k all|<key_index>
racadm sshpkauth -d -i svcacct -k all|<key_index>
```

## Input

- `-i <user_index>` — Index for the user.
- `-k [<key_index> | all]` — Index to assign the PK key being uploaded. all only works with the -v or -d options. <key_index> must be between 1 to 4 or all on iDRAC.
- `-t <PK_Key_Text>` — Key text for the SSH Public key.
- `-f <filename>` — File containing the key text to upload.
  NOTE: The -f option is not supported on SSH or serial RACADM.
- `-v` — View the key text for the index provided.
- `-d` — Delete the key for the index provided.

## Output/Example

Upload an invalid key to iDRAC User 2 in the first key space using a string.

```
$ racadm sshpkauth -i 2 -k 1 -t "This is invalid key Text"
```

```
ERROR: Key text appears to be corrupt
```

Upload a valid key to iDRAC User 2 in the first key space using a file.

```
$ racadm sshpkauth -i 2 -k 1 -f pkkey.key
```

```
Key file successfully uploaded.
```

Get all keys for User 2 on iDRAC.

```
$ racadm sshpkauth -v -i 2 -k all
```

```
********************* User ID 2 ******************
Key ID 1:
ssh-rsa
AAAAB3NzaC1yc2EAAAABIwAAAIEAzzy+k2npnKqVEXGXIzo0sbR6JgA5YNbWs3ekoxXV
fe3yJVpVc/
5zrrr7XrwKbJAJTqSw8Dg3iR4n3vUaP+lPHmUv5Mn55Ea6LHUslAXFqXmOdlThd
wilU2VLw/iRH1ZymUFnut8ggbPQgqV2L8bsUaMqb5PooIIvV6hy4isCNJU=
1024-bit RSA, converted from OpenSSH by xx_xx@xx.xx
Key ID 2:
Key ID 3:
Key ID 4:
```