# stack

## Install sets of packages

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

```bash
wo stack install --admin
```

## Install individual packages

### Main packages

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

### Additional packages

#### Adminer

```bash
wo stack install --adminer
```

#### PHPMyAdmin

```bash
wo stack install --phpmyadmin
```
