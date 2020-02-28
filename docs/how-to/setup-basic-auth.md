# Setup basic auth on site

## Prerequisites

Install Apache Utilities:

```
apt install apache2-utils
```

## Create password file

```
htpasswd -c /var/www/domain.tld/conf/nginx/.htpasswd username
```

You will be asked to supply and confirm a password for the user.


## Configure nginx

Edit `/var/www/domain.tld/conf/nginx/auth.conf`:

```
auth_basic "Restricted Access";
auth_basic_user_file /var/www/domain.tld/conf/nginx/.htpasswd;
```

Reload nginx:

```
nginx -t && service nginx reload
```