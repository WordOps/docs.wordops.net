# Getting Started

## Install WordOps

```bash
wget -qO wo wordops.se/tup && sudo bash wo
```

## Installing server stacks

### Method 1 : WordOps Full stack setup

The recommended method if you are going to host WordPress sites and want admin tools like phpMyAdmin or Monitoring.

```bash
wo stack install
```

This will setup the LEMP Stack (Nginx, PHP 7.2 and MariaDB) + the admin tools (phpMyAdmin, Netdata, Composer, WP-CLI, MySQLTuner, OpcacheGUI )

### Method 2 : Create your website

The recommended method if you only want to install the required stack to run your sites

```bash
wo site create site.tld --wp
```

This command will only setup the stack required to run WordPress (Nginx, PHP 7.2, MariaDB) and install WordPress.

Additional informations :

component              | Path                             |
-----------------------|----------------------------------|
Site files             | `/var/www/site.tld/htdocs`       |
wp-config.php          | `/var/www/site.tld/wp-config.php`|
Additional Nginx conf  | `/var/www/site.ltd/conf/nginx/`  |
Site access/error logs | `/var/www/site.tld/logs`         |
