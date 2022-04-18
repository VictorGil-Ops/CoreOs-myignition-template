# CoreOs-myignition-template

Producing an Ignition Config File - Core OS.

Use with OVA image for Vmware:

<https://getfedora.org/en/coreos/download?tab=metal_virtualized&stream=stable&arch=x86_64>

Documentation:

<https://docs.fedoraproject.org/en-US/fedora-coreos/producing-ign/>

## Commands:

```bash

# hash a passwd
echo 'toor' | openssl passwd -1 -salt core -stdin

# ssh key create
ssh-keygen -b 2048 -t rsa

# ign create
butane --pretty --strict coreos_template.bu > coreos_template.ign

# hash ign file
cat coreos_template.ign | gzip -9 | base64 -w0 -

```

## PASTE de HASH inline
