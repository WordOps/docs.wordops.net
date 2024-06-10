# stack

Manage server stack operations

Usage:

```bash
wo stack (command) [options]
```

|        subcommand         |        description         |
| :-----------------------: | :------------------------: |
| [install](#stack-install) |   Install WordOps stacks   |
| [upgrade](#stack-upgrade) |   Upgrade WordOps stack    |
| [migrate](#stack-migrate) |   Upgrade MariaDB stack    |
|  [remove](#stack-remove)  |     Uninstall packages     |
|   [purge](#stack-purge)   | Uninstall & purge packages |
|  [reload](#stack-reload)  |    Reload WordOps stack    |
| [restart](#stack-restart) |   Restart WordOps stack    |
|    [stop](#stack-stop)    |     Stop WordOps stack     |
|   [start](#stack-start)   |    Start WordOps stack     |

<!-- prettier-ignore     -->
!!! info

    Options are the same for `wo stack install`, `wo stack remove` and `wo stack purge`

<!-- prettier-ignore-end -->

Stack available are:

| options           | type          | description                                             |
| ----------------- | ------------- | ------------------------------------------------------- |
| `--web`           | Group         | Nginx, PHP, MySQL, WP-CLI                               |
| `--admin`         | Group         | phpMyAdmin, Adminer, Dashboard, Netdata, MySQLTuner ... |
| `--utils`         | Group         | OpcacheGUI, Webgrind, Anemometer                        |
| `--nginx`         | APT package   | nginx stack                                             |
| `--php`           | APT package   | Current supported PHP-FPM stack                         |
| `--php74`         | APT package   | PHP7.4-FPM stack                                        |
| `--php80`         | APT package   | PHP8.0-FPM stack                                        |
| `--php81`         | APT package   | PHP8.1-FPM stack                                        |
| `--php82`         | APT package   | PHP8.2-FPM stack                                        |
| `--php83`         | APT package   | PHP8.3-FPM stack                                        |
| `--mysql`         | APT package   | MariaDB stack                                           |
| `--redis`         | APT package   | Redis stack                                             |
| `--wpcli`         | Binary        | WP-CLI : WordPress CLI                                  |
| `--phpmyadmin`    | Web App       | phpMyAdmin : Web interface for MySQL                    |
| `--composer`      | Binary        | Composer : PHP dependencies manager                     |
| `--netdata`       | Binary        | Netdata : Real-time monitoring suite                    |
| `--dashboard`     | Web App       | WordOps dashboard                                       |
| `--extplorer`     | Web App       | eXtplorer Filemanager                                   |
| `--adminer`       | Web App       | adminer (phpmyadmin alternative)                        |
| `--fail2ban`      | APT package   | Fail2ban : Bruteforce protection                        |
| `--phpredisadmin` | Web App       | phpredisadmin : Web interface for Redis                 |
| `--proftpd`       | APT package   | proftpd stack : FTP server                              |
| `--mysqltuner`    | Binary        | MySQLTuner stack : MySQL tuning tool                    |
| `--ufw`           | APT package   | UFW : Firewall                                          |
| `--sendmail`      | APT package   | Sendmail MTA                                            |
| `--ngxblocker`    | Binary        | Ultimate Nginx bad bots blocker                         |
| `--nanorc`        | Binary        | Nano editor syntax highlighting                         |
| `--brotli`        | Configuration | Enable/Disable Brotli compression if Nginx is installed |

### Packages types

-   APT package are debian packages installed from APT repositories
-   Binaries are simple executables
-   Web App are php based applications

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

<!-- prettier-ignore -->
!!! info

    You can define MariaDB and PHP version to install by default in `/etc/wo/wo.conf`

<!-- prettier-ignore-end -->

Nginx, Current supported PHP version, MariaDB, Netdata, Fail2Ban, WordOps dashboard, phpMyAdmin, Adminer, MySQLtuner, OpcacheGUI

### Web

```bash
wo stack install --web
```

This will install Nginx, Current supported PHP version, MariaDB

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
| `--php74`      | Upgrade PHP 7.4 stack                     |
| `--php80`      | Upgrade PHP 8.0 stack                     |
| `--php81`      | Upgrade PHP 8.1 stack                     |
| `--php82`      | Upgrade PHP 8.2 stack                     |
| `--php83`      | Upgrade PHP 8.3 stack                     |
| `--mysql`      | Upgrade MySQL stack                       |
| `--wpcli`      | Upgrade WPCLI                             |
| `--redis`      | Upgrade Redis                             |
| `--netdata`    | Upgrade Netdata                           |
| `--dashboard`  | Upgrade WordOps Dashboard                 |
| `--composer`   | Upgrade Composer                          |
| `--phpmyadmin` | Upgrade phpMyAdmin                        |
| `--adminer`    | Upgrade Adminer                           |
| `--no-prompt`  | Upgrade Packages without any prompt       |
| `--force`      | Force Packages upgrade without any prompt |

`wo stack upgrade` make sure packages repositories are properly added, then it upgrade packages and for main stacks (Nginx, PHP-FPM & MySQL, Redis), it also update configurations from the templates included in the current WordOps release and apply optimizations (especially for MySQL & Redis)

Currently `wo stack upgrade --mysql` will only update the package from the current MariaDB repository, but will not perform upgrades between major releases (10.1 -> 10.3). For upgrade MariaDB, use `wo stack migrate --mariadb`.

## stack migrate

Upgrade MariaDB to the MariaDB release defined in `/etc/wo/wo.conf`

Usage :

```bash
wo stack migrate --mariadb [options]
```

Options :
`--force` : perform MariaDB upgrade without prompting for confirmation

<asciinema-player src="/images/wostackmigrate.cast" autoplay loop cols="125" rows="30"></asciinema-player>

## stack remove

Remove stacks (without removing configurations or data for APT packages)

Usage:

```bash
wo stack remove <stack> [options]
```

| options   | description                               |
| --------- | ----------------------------------------- |
| `--all`   | Remove all stacks at once                 |
| `--force` | Force install/remove/purge without prompt |

For APT packages, `wo stack remove` will just uninstall package without deleting their configurations or data. For binaries or web app, it will do the same than `wo stack purge`

## stack purge

Remove and purge stacks (including configurations and data)

<!-- prettier-ignore -->
!!! Warning

    Please be careful when using `wo stack purge` because it will remove APT packages but also purge all configurations or data, including MySQL databases, Redis databases or Nginx vhosts.

<!-- prettier-ignore-end -->

Usage:

```bash
wo stack purge <stack> [options]
```

| options | description                               |
| ------- | ----------------------------------------- |
| --all   | Remove all stacks at once                 |
| --force | Force install/remove/purge without prompt |

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

<asciinema-player src="/images/wostackstatus.cast" autoplay loop cols="125" rows="30"></asciinema-player>

Usage:

```bash
wo stack status [options]
```
