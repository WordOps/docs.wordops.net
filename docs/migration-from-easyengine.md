# Migration from EasyEngine v3

## Running WordOps install script

The first step to migrate from EasyEngine to WordOps is to run WordOps install script with the command :

```bash
curl -sL wops.cc | sudo -E bash -
```

!!! info
    Before installing WordOps, the install script will backup all previous EasyEngine configurations. You will find them after the installation in `/var/lib/wo-backup`.
