# Security recommendations

In this section, you will find few guides/tutorials about server security and what are the best ways to avoid security issues on your server(s)/site(s).

## Enable automatic installation of security upgrades

Debian and Ubuntu provide an automated security upgrades service with the package automatic installation of security upgrades unattended-upgrades. You can enable automatic installation of security upgrades with the command:

```bash
sudo dpkg-reconfigure -plow unattended-upgrades
```
