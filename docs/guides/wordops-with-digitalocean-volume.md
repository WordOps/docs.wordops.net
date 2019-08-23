# Use WordOps with DigitalOcean's volume

This is assuming you start with a brand new droplet and a brand new volume.

## Getting Started

1) Create Droplet.

2) Add volume –> Automatically format and mount


	*This guide is based as if your volume would be named: `YOUR-VOLUME`*

3)  Login to the droplet from the console, will ask for root password change.

4) Create directory `/var/www` where we will mount the volume and WordOps will be installed.

```bash
mkdir -p /var/www
```

## Mounting the volume

_Steps 5 and 6 are according to DigitalOcean -> Volumes -> 'More' tab of `YOUR-VOLUME` -> Config instructions_

5) Mount Digital Ocean's volume in `/var/www`

```bash
mount -o discard,defaults,noatime /dev/disk/by-id/scsi-0DO_Volume_YOUR-VOLUME /var/www
```

6) Change fstab so the volume will be mounted after a reboot

```bash
echo '/dev/disk/by-id/scsi-0DO_Volume_YOUR-VOLUME /var/www ext4 defaults,nofail,discard 0 0' | sudo tee -a /etc/fstab
```

## Installing WordOps

7) Install WordOps [According to One-Step Automated WordOps Install](https://docs.wordops.net/getting-started/installation-guide/ "One-Step Automated WordOps Install")

```bash
wget -qO wo wops.cc && sudo bash wo
```

You can enable autocomplete right after install with: `source /etc/bash_completion.d/wo_auto.rc`

8)  Install WordOps stacks (optional)

```bash
wo stack install
```

**And that's it!**

## Notes

- Just check with `df -h` or in netdata if `/var/www/` is shown with the correct size of your volume.
