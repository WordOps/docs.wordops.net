# maintenance

Update apt-cache and upgrade packages.

<asciinema-player src="/images/womaintenance.cast" autoplay loop cols="125" rows="30"></asciinema-player>

Usage:

```bash
wo maintenance
```

This command is equivalent to:

```bash
apt update
apt dist-upgrade
apt autoremove --purge
apt autoclean
```

Package update is performed in a non-interactive way, with the "--force-confold" policy, to never overwrite packages configurations.
