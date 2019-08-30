# Creating site

<video align="center" src="/images/wo-site.webm" width="720" autoplay="" loop="">
</video>

You can create site with WordOps by using the command `wo site create`.

WordOps will always:

- install required stack if needed
- configure Nginx vhost
- create site directory

WordOps can also:

- create the site database
- install WordPress (with or without caching)
- secure site with Let's Encrypt SSL certificate

You can see all the options available to create site in the command list [site create](/commands/site/#site-create)

## Additional informations

Component              | Path
---------------------- | ---------------------------------
Site files             | `/var/www/site.tld/htdocs`        |
wp-config.php          | `/var/www/site.tld/wp-config.php` |
Additional Nginx conf  | `/var/www/site.tld/conf/nginx/`   |
Site access/error logs | `/var/www/site.tld/logs`          |

## Examples

### Basic site

Basic html site

```bash
wo site create site.tld --html
```

Simple PHP site

```bash
wo site create site.tld --php
```

Simple PHP + MySQL site

```bash
wo site create site.tld --mysql
```

### WordPress site

Simple WordPress site

```bash
wo site create site.tld --wp
```

WordPress site with Nginx fastcgi_cache

```bash
wo site create site.tld --wpfc
```

WordPress site with Redis cache

```bash
wo site create site.tld --wpredis
```

### PHP 7.3

Simple PHP 7.3 + MySQL site

```bash
wo site create site.tld --mysql --php73
```

Simple PHP 7.3 site

```bash
wo site create site.tld --php73
```

Simple WordPress site with PHP 7.3

```bash
wo site create site.tld --wp --php73
```

### Let's Encrypt

WordPress site secured with Let's Encrypt

```bash
wo site create site.tld --wp -le
```

WordPress site on subdomain secure with Let's Encrypt

```bash
wo site create sub.site.tld --wp -le
```

**Since the release v3.9.8.4**, WordOps will automatically detect if the site is a domain or a subdomain, and will not issue a certificate for www alias with subdomains

WordPress site with PHP 7.3 and secured by Let's Encrypt

```bash
wo site create site.tld --wp --php73 -le
```

Create WordPress subdomain multisite secured with a Let's Encrypt Wildcard SSL certificate

!!! info
    More informations about wildcard SSL certificates our guide about [DNS API configuration](/how-to/configure-letsencrypt-dns-api-validation/)

```bash
wo site create site.tld --wpsubdomain --letsencrypt=wildcard --dns=dns_cf
```
