# WordPress sites migration

## Context

You want to migrate a WordPress site hosted on a server running EEv3 or WordOps to a new one running with WordOps.
The site you want to migrate was created with the flag `--wpredis`

In our example :

-   new server name is NEW-SRV with IP 10.0.0.1
-   the previous server is OLD-SRV with IP 192.168.0.1
-   site domain is mydomain.tld

## On the previous server (OLD-SRV)

### Dump WordPress database

Go into your site directory and dump WordPress database with WP-CLI

```bash
cd /var/www/mydomain.tld/htdocs
wp db export --allow-root
```

!!! info
    If WP-CLI isn't installed on your server, you can get it by running the following commands :
    ```bash
    curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
    chmod +x wp-cli.phar
    sudo mv wp-cli.phar /usr/local/bin/wp
    ```

## On the new server (NEW-SRV)

### Initial server update

```bash
apt-get update && apt-get dist-upgrade -y && apt-get autoremove --purge -y && apt-get autoclean
```

### Install WordOps and main stacks

```bash
wget -qO wo wops.cc && sudo bash wo
wo stack install
```

### Create an empty wordpress site with same domain

```bash
wo site create mydomain.tld --wpredis --vhostonly
```

### Setup a password-less ssh access between your servers

#### Generate SSH-Keys

If the user on the new server do not have ssh-keys yet, you can generate them with the following command :

```bash
ssh-keygen -t ed25519
```

Then just press enter to confirm ssh key path.
Your public ssh key should be available in the directory `~/.ssh/` ( `/root/.ssh/` if you are logged in as root )

#### Add SSH Public key to OLD-SRV

You can use the following command to automatically add the public SSH Key to the server :

```bash
ssh-copy-id root@192.168.0.1
```

Otherwise, you can still display the public ssh-key with the command `cat ~/.ssh/id_ed25519.pub` and copy it manually in the file `~/.ssh/authorized_keys` of the other server.

#### SSH Login without password

You should now be able to login from the server where you generated the SSH Keys to the other one without password :

```bash
ssh root@192.168.0.1
```

#### SSH Alias and config

If you prefer to use an alias to login to OLD-SRV rather than using the IP, or if you want to define a custom SSH port, you just have to create/edit the file `~/.ssh/config` and to define settings this way :

```bash
Host OLD-SRV
  Hostname 192.168.0.1
  Port 12345
```

Then you will be able to login with :

```bash
ssh root@OLD-SRV
```

or even with

```bash
ssh OLD-SRV
```

### Transfer files from OLD-SRV to NEW-SRV

To safely migrate files from OLD-SRV to NEW-SRV, we will use rsync because it's fast and secure (files transfer is done over SSH).
If you have configured password-less SSH login with the previous steps, and defined an alias into `~/.ssh/config` you can use the following command to copy files from OLD-SRV to NEW-SRV

```bash
rsync -avzh --progress --ignore-existing \
root@OLD-SRV:/var/www/mydomain.tld/htdocs/ \
/var/www/mydomain.tld/htdocs/
```

If you haven't created the file ~/.ssh/config and use custom SSH ports, you can define SSH port with rsync by using the following command :

```bash
rsync -avzh -e "ssh -p 12345" \
--progress --ignore-existing \
root@old_server_IP:/var/www/mydomain.tld/htdocs/ \
/var/www/mydomain.tld/htdocs/
```

#### Do not copy the file wp-config.php

With WordOps or EasyEngine v3, wp-config.php default path is `/var/www/mydomain.tld`. If you moved it into htdocs directory, it was probably transfered with rsync during the previous step. In this case remove it or rename it before importing the database on the new server, otherwise WP-CLI may not be able to login into MySQL.

Command example to keep previous wp-config.php file as backup :

```bash
mv /var/www/mydomain.tld/htdocs/wp-config.php /var/www/mydomain.tld/wp-config.php.bak
```

### Restore the database on NEW-SRV

We will use WP-CLI to easily import the database dump we have previously created on OLD-SRV.

```bash
cd /var/www/mydomain.tld/htdocs
wp db import my_domain_tld-2019-07-25-XX44z4.sql --allow-root
rm mydomain_co-2019-07-25-XX44z4.sql
```

### Let's Encrypt

If your site was secured with a Let's Encrypt SSL certificate, you can issue a new certificate on NEW-SRV with the command :

```bash
wo site update mydomain.tld -le
```
