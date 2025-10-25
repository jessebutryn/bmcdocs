# driverpack

## Description

Installs the driver pack for the operating system.

## Synopsis

```
racadm driverpack getinfo
racadm driverpack attach -i <index> -t <expose duration>
racadm driverpack detach
```

## Input

- `-i` — Index of the operating system
- `-t` — Exposed time duration in seconds. It is an optional parameter and the default value is 64800 seconds.

## Output/Example

Get information about available driver packs.

```
racadm driverpack getinfo
```

Attach the driver pack that matches the operating system.

```
racadm driverpack attach -i <OS Index> [-t <exposed time>]
```

Detach the driver pack.

```
racadm driverpack detach
```