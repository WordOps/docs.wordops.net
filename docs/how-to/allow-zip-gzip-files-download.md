# Allow zip & gzip files download

By default, WordOps deny access to zip, gzip and other archives format to avoid unwanted access to users's backup.
If you absolutely need to download those files, you can customize WordOps Nginx configuration.

## Edit Nginx configuration

### For all sites

For both WordPress and non-WordPress sites, the first file to edit is `/etc/nginx/common/locations-wo.conf` :

```bash
nano /etc/nginx/common/locations-wo.conf
```

You will find the following directive :

```nginx
# Deny backup extensions & log files and return 403 forbidden
location ~* "\.(old|orig|original|php#|php~|php_bak|save|swo|aspx?|tpl|sh|bash|bak?|cfg|cgi|dll|exe|git|hg|ini|jsp|log|mdb|out|sql|svn|swp|tar|rdf|gz|zip|bz2|7z|pem|asc|conf|dump)$" {
    deny all;
}
```

You just have to remove the files extensions you want to download. Then save your changes, and reload Nginx with `wo stack reload --nginx`.

To make sure your configuration will not be overwritted later, you have to create an empty file `/etc/nginx/common/locations-wo.conf.custom` :

```bash
touch /etc/nginx/common/locations-wo.conf.custom
```

### For WordPress sites

For WordPress sites, there is an additional configuration in `/etc/nginx/common/wpcommon-php7x.conf` where `7x` is the PHP version, it can be `72`, `73` or `74`.

Example, for a site running with PHP 7.4 :

```bash
nano /etc/nginx/common/wpcommon-php74.conf
```

You will find the following directive :

```nginx
    location ~* \.(php|gz|log|zip|tar|rar|xz)$ {
        #Prevent Direct Access Of PHP Files & Backups from Web Browsers
        deny all;
    }
```

Do the same than in the previous example, by removing files extensions you want to download, reload Nginx and create an empty `.custom` file to make sure your custom configuration will not be overwritted.