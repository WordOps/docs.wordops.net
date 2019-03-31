# maintenance

Update apt-cache and upgrade packages.

Usage :

```bash
wo maintenance
```

This command is equivalent to :

```bash
apt update
apt dist-upgrade
apt autoremove --purge
apt autoclean
```

Package update is performed in a non-interactive way, with the "--force-confold" policy, to never overwrite packages configurations.
