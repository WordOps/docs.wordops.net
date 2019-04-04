# site

Performs website specific operations

<video align="center" src="/images/wo-site.webm" width="720" autoplay loop>
</video>


Usage :

```bash
wo site (command) [options]
```

## site create

Usage :

```bash
wo site create  [<site_name>] [options]
```

### Basic sites

#### HTML site

To create simple html website use this command.

```bash
wo site create site.tld --html
```

#### PHP site

To create simple php website with no database use this command.

```bash
wo site create site.tld --php
```

#### PHP+MySQL site

To create simple php website with database use this command.

```bash
wo site create site.tld --mysql
```

NOTE: You can find MySQL database details in `/var/www/site.tld/wo-config.php`.

#### Proxy site

To create site with Proxy configuration you can use --proxy during site creation

```bash
wo site create site.tld --proxy=127.0.0.1:3000
```

This will create proxy site site.tld with proxy destination as 127.0.0.1:3000. Port is optional. Default port : 80.

### WordPress

Following are the WordPress website types you can create website based on Cache Mechanism

#### Standard sites

cache | PHP | example
-------- | -------------- | -------
no cache | PHP 7.2 | `wo site create site.tld --wp`
no cache | PHP 7.3 | `wo site create site.tld --wp --php73`
fastcgi_cache | PHP 7.2 | `wo site create site.tld --wpfc`
fastcgi_cache | PHP 7.3 | `wo site create site.tld --wpfc --php73`
wp-super-cache | PHP 7.2 | `wo site create site.tld --wpsc`
wp-super-cache | PHP 7.3 | `wo site create site.tld --wpsc --php73`
redis-cache | PHP 7.2 | `wo site create site.tld --wpredis`
redis-cache | PHP 7.3 | `wo site create site.tld --wpredis --php73`

#### Multisite subdirectory

cache          | PHP     | example
-------------- | ------- | ------------------------------------------------------
no cache       | PHP 7.2 | `wo site create site.tld --wpsubdir`
no cache       | PHP 7.3 | `wo site create site.tld --wpsubdir --php73`
fastcgi_cache  | PHP 7.2 | `wo site create site.tld --wpsubdir --wpfc`
fastcgi_cache  | PHP 7.3 | `wo site create site.tld --wpsubdir --wpfc --php73`
wp-super-cache | PHP 7.2 | `wo site create site.tld --wpsubdir --wpsc`
wp-super-cache | PHP 7.3 | `wo site create site.tld --wpsubdir --wpsc --php73`
redis-cache    | PHP 7.2 | `wo site create site.tld --wpsubdir --wpredis`
redis-cache    | PHP 7.3 | `wo site create site.tld --wpsubdir --wpredis --php73`

#### Multisite subdomain

cache          | PHP     | example
-------------- | ------- | ------------------------------------------------------
no cache       | PHP 7.2 | `wo site create site.tld --wpsubdom`
no cache       | PHP 7.3 | `wo site create site.tld --wpsubdom --php73`
fastcgi_cache  | PHP 7.2 | `wo site create site.tld --wpsubdir --wpfc`
fastcgi_cache  | PHP 7.3 | `wo site create site.tld --wpsubdom --wpfc --php73`
wp-super-cache | PHP 7.2 | `wo site create site.tld --wpsubdom --wpsc`
wp-super-cache | PHP 7.3 | `wo site create site.tld --wpsubdom --wpsc --php73`
redis-cache    | PHP 7.2 | `wo site create site.tld --wpsubdom --wpredis`
redis-cache    | PHP 7.3 | `wo site create site.tld --wpsubdom --wpredis --php73`

#### Extra settings

Define WordPress administrator user To define wordpress administrator user during site creation use

```bash
wo site create site.tld --user=admin
```

This will create admin as administrator user in wordpress during installation. If not defined it will take git user name.

Define WordPress administrator password To define wordpress administrator password during site creation use

```bash
wo site create site.tld --pass=password
```

This will set defined password as administrator password. If not defined it will generate random pasword for administrator. If you have special characters, you can quote them using single quotes like this :

--pass='my$secret&' Define WordPress administrator email To define wordpress administrator email during site creation use

```bash
wo site create site.tld --email=wo@site.tld
```

This will set defined email as administrator email. If not defined it will set git email as administrator email.

### Let's Encrypt

WordOps supports Let's Encrypt out of the box.

```bash
wo site create site.tld --letsencrypt
```

This command will issue a certificate for site.tld + www.site.tld.

But WordOps also supports issuing Let's Encrypt certificates with subdomains.

```bash
wo site create site.tld --letsencrypt=subdomain
```

You can add --letsencrypt to any other flag.

### PHP 7.3

To create site with PHP 7.3 you can use --php73 during site creation

For example, you can create WordPress site running on PHP 7.3 using following command:

```bash
wo site create site.tld --wp --php73
```

To create simple php(with v7.3) website with no database use this command.

```bash
wo site create site.tld --php73
```

## site update

Update site configuration

Usage :

```bash
wo site update  [<site_name>] [options]
```

options | description
------- | ------------
`--html` | update to html site
`--php` | update to php site
`--mysql` | update to MySQL + PHP site
`--php73` | update site to PHP 7.3
`--php73=off` | disable PHP 7.3
`--wp` | update site to WordPress without cache
`--wpfc` | update site to WordPress with fastcgi_cache
`--wpsc` | update site to WordPress with wp-super-cache
`--wpredis` | update site to WordPress with redis-cache

## site delete

Usage :

```bash
wo site delete  [<site_name>] [options]
```

options       | description
------------- | --------------------------------------------
`--no-prompt`      | delete website without confirmation prompt
`--files`       | delete only website files
`--db`     | delete only database
