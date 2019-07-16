# stack

Manage server stack operations

Usage :

```bash
wo stack (command) [options]
```

subcommand                   | description
------------------------- | -----------------------------------------------------
[install](#stack-install)       | Install packages
[reload](#stack-reload)         | Reload WordOps stack
[remove](#stack-remove)         | Uninstall packages
[purge](#stack-purge)           | Uninstall & purge packages
[restart](#stack-restart)       | Restart WordOps stack
[stop](#stack-stop)             | Stop WordOps stack
[upgrade](#stack-upgrade)       | Upgrade WordOps stack
[start](#stack-start)           | Start WordOps stack

## stack install

<video align="center" src="/images/wo-stack.webm" width="720" autoplay loop></video>

Usage :

```bash
wo stack install [options]
```

### Web

This will install Nginx, PHP 7.2, MariaDB

```bash
wo stack install
```

or

```bash
wo stack install web
```

### Admin tools

WordOps backend with WordOps-Dashboard, PHPmyAdmin, Adminer, MemcachedAdmin etc..

```bash
wo stack install --admin
```

### Individual packages

#### Nginx

```bash
wo stack install --nginx
```

#### PHP 7.2

```bash
wo stack install --php
```

#### MariaDB (MySQL)

```bash
wo stack install --mysql
```

#### Adminer

```bash
wo stack install --adminer
```

#### PHPMyAdmin

```bash
wo stack install --phpmyadmin
```

#### Netdata

```bash
wo stack install --netdata
```