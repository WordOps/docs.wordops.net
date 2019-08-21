# Use WordOps in DigitalOcean's volume
This is assuming you start with a brand new droplet and a brand new volume.

1. Create Droplet.
2. Add volume –> Automatically format and mount. This guide is based as if your volume would be named: `YOUR-VOLUME`
3. Login to the droplet from the console, will ask for root password change.

4. Install WordOps [(According to One-Step Automated WordOps Install)](https://docs.wordops.net/getting-started/installation-guide/ "One-Step Automated WordOps Install")
```sh
$ wget -qO wo wops.cc && sudo bash wo
```
You can enable autocomplete right after install with: `$ source /etc/bash_completion.d/wo_auto.rc`
5. Install WordOps stacks (optional)
```sh
$ wo stack install
```
6. Rename `/var/www/`  to something else, I use: `/var/NOTwww/`
```sh
$ mv /var/www/ /var/NOTwww/
```
7. Create `/var/www/`
```sh
$ mkdir -p /var/www/
```
*Steps 8 and 9 are according to DigitalOcean -> Volumes -> 'More' tab of `YOUR-VOLUME` -> Config instructions*

8. Mount Digital Ocean's volume in `/var/www/`
```sh
$ mount -o discard,defaults,noatime /dev/disk/by-id/scsi-0DO_Volume_YOUR-VOLUME /var/www/
```

9. Change fstab so the volume will be mounted after a reboot
```sh
$ echo '/dev/disk/by-id/scsi-0DO_Volume_YOUR-VOLUME /var/www/ ext4 defaults,nofail,discard 0 0' | sudo tee -a /etc/fstab
```
10. Merge folders `/var/NOTwww/` (where WordOps was installed) with `/var/www/` (mounted volume).
```sh
$ rsync -av /var/NOTwww/ /var/www/
```
11. Delete `/var/NOTwww/`
```sh
$ rm -rf /var/NOTwww/
```
**And that's it!**
### Notes
* You should def check if `/var/www/` is shown in netdata witht the correct size.
* Only kinda problem I had is that I wasn't able to login to the WordOps dashboard after the first reboot, I thought WordOps wasn't working or that there was something wrong with the volume but after a couple of minutes evrything was working great.
