# Getting Started

## Install WordOps

```bash
wget -qO wo wordops.se/tup && sudo bash wo
```

## Create your first WordPress site

```bash
wo site create site.tld --wp
```

This command will install Nginx, PHP, MariaDB (MySQL), then it will download and configure WordPress.

Additional informations :

- site files path is `/var/www/site.tld/htdocs`
- wp-config.php path is `/var/www/site.tld/wp-config.php`
- additional nginx configurations path is `/var/www/site.ltd/conf/nginx/`
- nginx logs path is `/var/www/site.tld/logs`
