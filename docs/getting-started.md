# Getting Started

## Install WordOps

You can use our automated installer to setup WordOps. Additional installation method are available in our [installation guide](installation-guide.md)

```bash
wget -qO wo wordops.se/tup && sudo bash wo
```

During the installation, you will be prompt for an username and an email address. WordOps need those informations to configure Git version control and to use it for saving server configurations.
Your informations will only be stored in the file .gitconfig.

## Installing server stacks

### Method 1 : WordOps Full stack setup (recommended)

```bash
wo stack install
```

This will setup the LEMP Stack (Nginx, PHP 7.2 and MariaDB) and the admin tools (phpMyAdmin, Netdata, Composer, WP-CLI, MySQLTuner, OpcacheGUI )

### Method 2 : Only install required stack

If you prefer to only install required stack to run your sites, you can directly use the command `wo site create`.

For example, the following command will only install Nginx :

```bash
wo site create site.tld --html
```

And this command will only install Nginx and PHP 7.2 :

```bash
wo site create site.tld --php
```

### Additional informations

Component              | Path                             |
-----------------------|----------------------------------|
Site files             | `/var/www/site.tld/htdocs`       |
wp-config.php          | `/var/www/site.tld/wp-config.php`|
Additional Nginx conf  | `/var/www/site.tld/conf/nginx/`  |
Site access/error logs | `/var/www/site.tld/logs`         |

## Creating site

<video align="center" src="/images/wo-site.webm" width="720" autoplay="" loop="">
</video>

You can create site with WordOps by using the command `wo site create`.

WordOps will always :

- install required stack if needed
- configure Nginx vhost
- create site directory

WordOps can also :

- create the site database
- install WordPress (with or without caching)
- secure site with Let's Encrypt SSL certificate

You can see all the options available to create site in the command list [site create](commands/site.md#site-create)

### PHP 7.3 support

To create site running with PHP 7.3, you can add the argument `--php73` with the command `wo site create` and `wo site update`.

Here few examples :

#### WordPress site

```bash
wo site create site.tld --wp --php73
```

This command will create site.tld running with PHP 7.3 and install WordPress.

#### MySQL + PHP site

```bash
wo site create site.tld --mysql --php73
```

### Let's Encrypt SSL certificates

To secure your site with Let's Encrypt SSL certificate, you can use the argument `--letsencrypt` or `--le` with the command `wo site create` or with the command `wo site update` when it's an existing site.

WordOps always check if a site is already secured with Let's Encrypt before issuing a certificate, and it also configure the certificate with Nginx and add the proper redirection from http to https.

Here few examples :

#### Create SSL site

```bash
wo site create site.tld --wp --letsencrypt
```

This command will create site.tld and issue a certificate for site.tld and www.site.tld

#### Create subdomain SSL site

```bash
wo site create sub.site.tld --wp --letsencrypt=subdomain
```

This command will create sub.site.tld and issue a certificate only for sub.site.tld

#### Secure existant site

```bash
wo site update site.tld --letsencrypt
```

This command will issue a certificate for site.tld and www.site.tld.
