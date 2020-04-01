# Setup basic auth on site

## Prerequisites

Install Apache Utilities:

```bash
apt install apache2-utils
```

## Create password file

```bash
htpasswd -c /var/www/domain.tld/conf/nginx/.htpasswd username
```

You will be asked to supply and confirm a password for the user.

## Configure nginx

Edit `/var/www/domain.tld/conf/nginx/auth.conf`:

```bash
auth_basic "Restricted Access";
auth_basic_user_file /var/www/domain.tld/conf/nginx/.htpasswd;
```

Reload nginx:

```bash
wo stack reload --nginx
```
