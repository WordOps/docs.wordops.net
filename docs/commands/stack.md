# stack

Manage server stack operations

Usage:

```bash
wo stack (command) [options]
```

| subcommand                | description                |
| ------------------------- | -------------------------- |
| [install](#stack-install) | Install WordOps stacks     |
| [upgrade](#stack-upgrade) | Upgrade WordOps stack      |
| [remove](#stack-remove)   | Uninstall packages         |
| [purge](#stack-purge)     | Uninstall & purge packages |
| [reload](#stack-reload)   | Reload WordOps stack       |
| [restart](#stack-restart) | Restart WordOps stack      |
| [stop](#stack-stop)       | Stop WordOps stack         |
| [start](#stack-start)     | Start WordOps stack        |

!!! info
    Options are the same for `wo stack install`, `wo stack remove` and `wo stack purge`

Stack available are:

| options           | type        | description                                             |
| ----------------- | ----------- | ------------------------------------------------------- |
| `--web`           | Group       | Nginx, PHP, MySQL, WP-CLI                               |
| `--admin`         | Group       | phpMyAdmin, Adminer, Dashboard, Netdata, MySQLTuner ... |
| `--utils`         | Group       | OpcacheGUI, Webgrind, Anemometer                        |
| `--nginx`         | APT package | nginx stack                                             |
| `--php`           | APT package | PHP7.2-FPM stack                                        |
| `--php73`         | APT package | PHP7.3-FPM stack                                        |
| `--mysql`         | APT package | MariaDB stack                                           |
| `--redis`         | APT package | Redis stack                                             |
| `--wpcli`         | Binary      | WP-CLI : WordPress CLI                                  |
| `--phpmyadmin`    | Web App     | phpMyAdmin : Web interface for MySQL                    |
| `--composer`      | Binary      | Composer : PHP dependencies manager                     |
| `--netdata`       | Binary      | Netdata : Real-time monitoring suite                    |
| `--dashboard`     | Web App     | WordOps dashboard                                       |
| `--extplorer`     | Web App     | eXtplorer Filemanager                                   |
| `--adminer`       | Web App     | adminer (phpmyadmin alternative)                        |
| `--fail2ban`      | APT package | Fail2ban : Bruteforce protection                        |
| `--phpredisadmin` | Web App     | phpredisadmin : Web interface for Redis                 |
| `--proftpd`       | APT package | proftpd stack : FTP server                              |
| `--mysqltuner`    | Binary      | MySQLTuner stack : MySQL tuning tool                    |
| `--ufw`           | APT package | UFW : Firewall                                          |
| `--sendmail`      | APT package | Sendmail MTA                                            |
| `--ngxblocker`    | Binary      | Ultimate Nginx bad bots blocker                         |

### Packages types

- APT package are debian packages installed from APT repositories
- Binaries are simple executables
- Web App are php based applications

## stack install

Usage:

```bash
wo stack install [options]
```

Without options, the stack `--web`, `--admin`, `--utils` will be installed

### Recommended install

```bash
wo stack install
```

<asciinema-player src="/images/stackinstall.cast" autoplay loop cols="125" rows="30"></asciinema-player>

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

Upgrade stack safely and apply new configurations and optimizations

Usage:

```bash
wo stack upgrade [options]
```

| options        | description                               |
| -------------- | ----------------------------------------- |
| `--all`        | Upgrade all stack                         |
| `--web`        | Upgrade web stack                         |
| `--admin`      | Upgrade admin tools stack                 |
| `--nginx`      | Upgrade Nginx stack                       |
| `--php`        | Upgrade PHP 7.2 stack                     |
| `--php73`      | Upgrade PHP 7.3 stack                     |
| `--mysql`      | Upgrade MySQL stack                       |
| `--wpcli`      | Upgrade WPCLI                             |
| `--redis`      | Upgrade Redis                             |
| `--netdata`    | Upgrade Netdata                           |
| `--dashboard`  | Upgrade WordOps Dashboard                 |
| `--composer`   | Upgrade Composer                          |
| `--phpmyadmin` | Upgrade phpMyAdmin                        |
| `--no-prompt`  | Upgrade Packages without any prompt       |
| `--force`      | Force Packages upgrade without any prompt |

`wo stack upgrade` make sure packages repositories are properly added, then it upgrade packages and for main stacks (Nginx, PHP-FPM & MySQL, Redis), it also update configurations from the templates included in the current WordOps release and apply optimizations (especially for MySQL & Redis)

Currently `wo stack upgrade --mysql` will only update the package from the current MariaDB repository, but will not perform upgrades between major releases (10.1 -> 10.3), mostly because there is a risk of failure when upgrading MariaDB, and we will have to run more tests to make sure our upgrading process is stable and will not impact your sites availability.

## stack remove

Remove stacks (without removing configurations or data for APT packages)

Usage:

```bash
wo stack remove <stack> [options]
```

| options           | description                                 |
| ----------------- | ------------------------------------------- |
| `--all`           | Remove all stacks at once                   |
| `--force`         | Force install/remove/purge without prompt   |

For APT packages, `wo stack remove` will just uninstall package without deleting their configurations or data. For binaries or web app, it will do the same than `wo stack purge`

## stack purge

Remove and purge stacks (including configurations and data)

!!! Warning
    Please be careful when using `wo stack purge` because it will remove APT packages but also purge all configurations or data, including MySQL databases, Redis databases or Nginx vhosts.

Usage:

```bash
wo stack purge <stack> [options]
```

| options         | description                                 |
| --------------- | ------------------------------------------- |
| --all           | Remove all stacks at once                   |
| --force         | Force install/remove/purge without prompt   |

## stack restart

Restart Stack service

Usage:

```bash
wo stack restart [options]
```

## stack reload

Reload Stack service

Usage:

```bash
wo stack reload [options]
```

## stack start

Start Stack service

Usage:

```bash
wo stack start [options]
```

## stack stop

Stop Stack service

Usage:

```bash
wo stack stop [options]
```

## stack status

Display Stack service status

Usage:

```bash
wo stack status [options]
```
