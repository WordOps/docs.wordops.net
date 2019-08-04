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


| options           | description                                                                   |
|-------------------|-------------------------------------------------------------------------------|
| `--web`           | install web  stack (Nginx, PHP, MySQL, WP-CLI)                                |
| `--admin`         | install admin stack (phpMyAdmin, Adminer, Dashboard, Netdata, MySQLTuner ...) |
| `--nginx`         | install nginx stack                                                           |
| `--php`           | install PHP7.2-FPM stack                                                      |
| `--php73`         | install PHP7.3-FPM stack                                                      |
| `--mysql`         | install MariaDB stack                                                         |
| `--redis`         | install Redis stack                                                           |
| `--wpcli`         | install WP-CLI                                                                |
| `--phpmyadmin`    | install phpMyAdmin                                                            |
| `--composer`      | install Composer                                                              |
| `--netdata`       | install Netdata                                                               |
| `--dashboard`     | install WordOps dashboard                                                     |
| `--adminer`       | install adminer                                                               |
| `--fail2ban`      | install fail2ban                                                              |
| `--utils`         | install several admin tools                                                   |
| `--phpredisadmin` | install phpredisadmin                                                         |
| `--proftpd`       | install proftpd stack                                                         |


### Recommended install

```bash
wo stack install
```

<video align="center" src="/images/wo-stack.webm" width="720" autoplay loop></video>

This will install the `--web` stack and `--admin` stack.

Nginx, PHP 7.2, MariaDB, Netdata, WordOps dashboard, phpMyAdmin, Adminer, MySQLtuner, OpcacheGUI

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
