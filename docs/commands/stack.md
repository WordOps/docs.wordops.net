# stack

Manage server stack operations

<video align="center" src="/images/wo-stack.webm" width="720" autoplay ></video>

Usage :

```bash
wo stack (command) [options]
```

## stack install

Usage :

```bash
wo stack install [options]
```

### Web

This will install Nginx, PHP 7.2, MariaDB & additional tools available on port 22222

```bash
wo stack install
```

or

```bash
wo stack install web
```

### Admin tools

WordOps backend with PHPmyAdmin, Adminer, MemcachedAdmin etc..

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