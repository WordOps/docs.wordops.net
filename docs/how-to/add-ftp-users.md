# How to add FTP users

WordOps ProFTPd stack provide the ability to install and configure automatically ProFTPd and to secure it with a self-signed certificates (same encryption level than any other valid certificate). You can install it with :

```bash
wo stack install --proftpd
```

But WordOps do not provide an easy way to add FTP users yet. So this short guide will explain how to add a new FTP user.

!!! info
    This guide explain how to add new users safely, which means :

    - users will not be able to login via SSH or any shell
    - users will only have access to a single site files

## Adding a new user

In this example we will add a new user named `wordops`, and he will only be able to access to all files of the site wordops.net :

```bash
adduser --home /var/www/wordops.net/htdocs/ \
--shell /bin/false --ingroup www-data wordops
```

There is another step to allow our new user to upload/edit files :

```bash
chmod -R g+rw /var/www/wordops.net/htdocs
```

## Firewall configuration

If you are using UFW, you must allow the FTP port and some passive ports:

```
ufw allow 21
ufw allow 49000:50000/tcp
```
