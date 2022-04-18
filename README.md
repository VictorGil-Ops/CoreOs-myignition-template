# CoreOs-myignition-template

Producing an Ignition Config File - Core OS.

| user     | passwd |
| -------- | -------|
| core     | toor   |

Use with OVA image for Vmware:

<https://getfedora.org/en/coreos/download?tab=metal_virtualized&stream=stable&arch=x86_64>

Documentation:

<https://docs.fedoraproject.org/en-US/fedora-coreos/producing-ign/>

## Commands

```bash

# hash a passwd
echo 'toor' | openssl passwd -1 -salt core -stdin

# ssh key create
ssh-keygen -b 2048 -t rsa

# ign create
butane --pretty --strict coreos_template.bu > coreos_template.ign

# hash ign file
cat local_coreos_template.ign | gzip -9 | base64 -w0 -

```

## PASTE de HASH inline

Hash and use the `local_* ign file`, the encoding is `gzip+base64`

![](https://github.com/VictorGil-Ops/CoreOs-myignition-template/blob/main/images/vmware_ova_deploy.png)

## HASH for this local ign (local_coreos_template.ign), use directly

```bash

H4sIAAAAAAACA02PMQ+CQAyFd34FuVnuTNhYHRzZXA1eKjThrqRXNIbcf7eCGKfmfX3pe12KsjTYRxSkaJpyUa3EU7xj/9NKGKax8/CHFCaaeWVmEJlS4xx3T9ujDPNtTsB6RiCK9RTcBb0Qn3Gs2im5EzG0qQqvPbsSCJog4EKH0TEEErh6tVG67jurbvONz+vMh63wAzhtH5ja1vb4ceUiF2/iXTsC4AAAAA==

```

## Change hostname and IP

```bash

# hostname
hostnameclt set-hostname master-node

# ip
nmcli connection show 

nmcli connection mod 'Wired connection 1' \
ipv4.method manual \
connection.autoconnect yes \
ipv4.addresses 192.168.205.210/24 \
ipv4.gateway 192.168.205.2 \
ipv4.dns 1.1.1.1 \
+ipv4.dns 1.0.0.1

# reboot
systemctl reboot

```
