# WordOps commands

## Overview

| command | feature | example |
|-|---------|-|
| [site](#site) |  [create](#create), [update](#update), [delete](#delete), list sites | `wo site create site.tld --wp` |
| [stack](#stack) | install/remove WordOps server stacks | `wo stack install --nginx` |
| [debug](#debug) | commands to do server level debugging | `wo debug site.tld --php` |
| [clean](#clean) | clean Wordops cache backend | `wo clean --fastcgi` |
| [info](#info) | display server stack informations | `wo info --nginx` |
| [log](#log) | perform operation on logs | `wo log show --nginx` |
| [secure](#secure) | manage WordOps backend authentification | `wo secure --auth` |
| [maintenance](#maintenance) | perform server package updates | `wo maintenance`
| [update](#update) | update WordOps | `wo update` |

## site

### create

#### Basic sites

##### HTML site

To create simple html website use this command.

```bash
wo site create example.com --html
```

##### PHP site

To create simple php website with no database use this command.

```bash
wo site create example.com --php
```

##### PHP+MySQL site

To create simple php website with database use this command.

```bash
wo site create example.com --mysql
```

NOTE: You can find MySQL database details in wo-config.php file.

##### Proxy site

To create site with Proxy configuration you can use --proxy during site creation

```bash
wo site create example.com --proxy=host[:port]
```

Here port is optional and default value is 80.

For example,

```bash
wo site create example.com --proxy=1.2.3.4
```

This will create proxy site example.com with proxy destination as 1.2.3.4

#### WordPress

Following are the WordPress website types you can create website based on Cache Mechanism

##### Standard sites


 cache          | PHP     | example
-------- -------------- | ------- | -------------------------------------------
 no cache       | PHP 7.2 | `wo site create site.tld --wp`
          no cache       | PHP 7.3 | `wo site create site.tld --wp --php73`
          fastcgi_cache  | PHP 7.2 | `wo site create site.tld --wpfc`
          fastcgi_cache  | PHP 7.3 | `wo site create site.tld --wpfc --php73`
          wp-super-cache | PHP 7.2 | `wo site create site.tld --wpsc`
          wp-super-cache | PHP 7.3 | `wo site create site.tld --wpsc --php73`
          redis-cache    | PHP 7.2 | `wo site create site.tld --wpredis`
          redis-cache    | PHP 7.3 | `wo site create site.tld --wpredis --php73`


##### Multisite subdirectory

 cache          | PHP     | example
 -------------- | ------- | -------------------------------------------
 no cache       | PHP 7.2 | `wo site create site.tld --wpsubdir`
          no cache       | PHP 7.3 | `wo site create site.tld --wpsubdir --php73`
          fastcgi_cache  | PHP 7.2 | `wo site create site.tld --wpsubdir --wpfc`
          fastcgi_cache  | PHP 7.3 | `wo site create site.tld --wpsubdir --wpfc --php73`
          wp-super-cache | PHP 7.2 | `wo site create site.tld --wpsubdir --wpsc`
          wp-super-cache | PHP 7.3 | `wo site create site.tld --wpsubdir --wpsc --php73`
          redis-cache    | PHP 7.2 | `wo site create site.tld --wpsubdir --wpredis`
          redis-cache    | PHP 7.3 | `wo site create site.tld --wpsubdir --wpredis --php73`

##### Multisite subdomain

 cache          | PHP     | example
-------------- | ------- | -------------------------------------------------
 no cache       | PHP 7.2 | `wo site create site.tld --wpsubdom`
          no cache       | PHP 7.3 | `wo site create site.tld --wpsubdom --php73`
          fastcgi_cache  | PHP 7.2 | `wo site create site.tld --wpsubdir --wpfc`
          fastcgi_cache  | PHP 7.3 | `wo site create site.tld --wpsubdom --wpfc --php73`
          wp-super-cache | PHP 7.2 | `wo site create site.tld --wpsubdom --wpsc`
          wp-super-cache | PHP 7.3 | `wo site create site.tld --wpsubdom --wpsc --php73`
          redis-cache    | PHP 7.2 | `wo site create site.tld --wpsubdom --wpredis`
          redis-cache    | PHP 7.3 | `wo site create site.tld --wpsubdom --wpredis --php73`

##### Extra settings

Define WordPress administrator user To define wordpress administrator user during site creation use

```bash
wo site create example.com --user=admin
```

This will create admin as administrator user in wordpress during installation. If not defined it will take git user name.

Define WordPress administrator password To define wordpress administrator password during site creation use

```bash
wo site create example.com --pass=password
```

This will set defined password as administrator password. If not defined it will generate random pasword for administrator. If you have special characters, you can quote them using single quotes like this :

--pass='my$secret&' Define WordPress administrator email To define wordpress administrator email during site creation use

```bash
wo site create example.com --email=wo@site.tld
```

This will set defined email as administrator email. If not defined it will set git email as administrator email.

#### Let's Encrypt

WordOps supports Let's Encrypt out of the box.

```bash
wo site create site.tld --letsencrypt
```

This command will issue a certificate for site.tld + www.site.tld.

But WordOps also supports issuing Let's Encrypt certificates with subdomains.

```bash
wo site create example.com --letsencrypt=subdomain
```

You can add --letsencrypt to any other flag.

#### PHP 7.3

To create site with PHP 7.3 you can use --php73 during site creation

For example, you can create WordPress site running on PHP 7.3 using following command:

```bash
wo site create example.com --wp --php73
```

To create simple php(with v7.3) website with no database use this command.

```bash
wo site create example.com --php73
```

### update



--------------------------------------------------------------------------------

### delete

To delete site created with EasyEngine (wo) use

```bash
wo site delete example.com</code>
```

#### Delete website without prompt

```bash
wo site delete example.com --no-prompt</code>
```

#### Delete website webroot only

```bash
wo site delete example.com --files</code>
```

#### Delete website database only

```bash
wo site delete example.com --db</code>
```

## stack

### install

#### Web

This will install Nginx, PHP 7.2, MariaDB & additional tools available on port 22222

```bash
wo stack install
```

or

```bash
wo stack install web
```

#### Admin tools

```bash
wo stack install --admin
```

#### Individual packages

##### Nginx

```bash
wo stack install --nginx
```

##### PHP 7.2

```bash
wo stack install --php
```

##### MariaDB (MySQL)

```bash
wo stack install --mysql
```

##### Adminer

```bash
wo stack install --adminer
```

##### PHPMyAdmin

```bash
wo stack install --phpmyadmin
```

### debug

### clean

### info

```bash


### log

### secure

### maintenance

Update servers packages :

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

Package update is performed in a non-interactive way, with the policy of never overwriting packages configuration with new configuration.

### update

Update WordOps to the latest release with the command :

```bash
wo update
```