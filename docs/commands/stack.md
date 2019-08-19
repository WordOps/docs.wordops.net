# stack

Manage server stack operations

Usage :

```bash
wo stack (command) [options]
```

subcommand                | description
--------------------------|---------------------------
[install](#stack-install) | Install packages
[reload](#stack-reload)   | Reload WordOps stack
[remove](#stack-remove)   | Uninstall packages
[purge](#stack-purge)     | Uninstall & purge packages
[restart](#stack-restart) | Restart WordOps stack
[stop](#stack-stop)       | Stop WordOps stack
[upgrade](#stack-upgrade) | Upgrade WordOps stack
[start](#stack-start)     | Start WordOps stack

## stack install

Usage :

```bash
wo stack install [options]
```

Without options, the stack `--web`, `--admin`, `--utils` will be installed


| options           | type        | description                                             |
| ----------------- | ----------- | ------------------------------------------------------- |
| `--web`           | Group       | Nginx, PHP, MySQL, WP-CLI                               |
| `--admin`         | Group       | phpMyAdmin, Adminer, Dashboard, Netdata, MySQLTuner ... |
| `--nginx`         | APT package | install nginx stack                                     |
| `--php`           | APT package | install PHP7.2-FPM stack                                |
| `--php73`         | APT package | install PHP7.3-FPM stack                                |
| `--mysql`         | APT package | install MariaDB stack                                   |
| `--redis`         | APT package | install Redis stack                                     |
| `--wpcli`         | Binary      | install WP-CLI                                          |
| `--phpmyadmin`    | Web App     | install phpMyAdmin                                      |
| `--composer`      | Binary      | install Composer                                        |
| `--netdata`       | Binary      | install Netdata                                         |
| `--dashboard`     | Web App     | install WordOps dashboard                               |
| `--adminer`       | Web App     | install adminer                                         |
| `--fail2ban`      | APT package | install fail2ban                                        |
| `--utils`         | Group       | OpcacheGUI, Webgrind, Anemometer                        |
| `--phpredisadmin` | Webp App    | install phpredisadmin                                   |
| `--proftpd`       | APT package | install proftpd stack                                   |

### Packages types

- APT package are debian packages installed from APT repositories
- Binaries are simple executables
- Web App are php based applications

### Recommended install

```bash
wo stack install
```

<video align="center" src="/images/wo-stack.webm" width="720" autoplay loop></video>

This will install the `--web` stack and `--admin` stack.

Nginx, PHP 7.2, MariaDB, Netdata, Fail2Ban, WordOps dashboard, phpMyAdmin, Adminer, MySQLtuner, OpcacheGUI

### Web

```bash
wo stack install --web
```

This will install Nginx, PHP 7.2, MariaDB

### Admin tools

WordOps backend with WordOps-Dashboard, PHPmyAdmin, Adminer, OpcacheGUI etc..

```bash
wo stack install --admin
```

After installing the Admin stack, WordOps dashboard will be available on https://YOUR.SERVER.IP:22222 with the credentials displayed during the stack installation.

## stack upgrade

Upgrade stack safely

Usage :

```bash
wo stack upgrade [options]
```

### Options

#### Nginx

Upgrade Nginx

```bash
wo stack upgrade --nginx
```
