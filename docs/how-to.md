# How to ... ?

## Questions overview

- [How to set default language for WordPress install ?](/how-to/wp-language/)
- [How to secure WordOps backend with Let's Encrypt SSL certificate ?](/how-to/secure-22222/)
- [How to renew Let's Encrypt Certificates ?](#renew-a-lets-encrypt-ssl-certificates-with-wordops)
- [How to configure Let's Encrypt DNS API validation](/how-to/configure-letsencrypt-dns-api-validation/)
- [How to get an A+ grade on ssllabs with Wordops ?](how-to/get-a-plus-grade-ssllabs.md)
- [How to add FTP users](how-to/add-ftp-users.md)
- [How to install HWE stacks on Ubuntu](how-to/ubuntu-lts-hwe-stacks.md)
- [How to use a Remote MySQL server with WordOps](how-to/remote-mysql-server.md)
- [How to automate WordPress post-install tasks](how-to/post-install-wp.md)
- [How to allow zip & gzip files download](how-to/allow-zip-gzip-files-download.md)
- [How to setup basic http-auth on sites](how-to/setup-basic-auth.md)
- [How to automated WordOps installation](how-to/automated-wordops-install.md)

## Other questions

### Get a list of WordOps commands

To get the list of WordOps commands, you can use the command:

```bash
wo
```

Then for any subcommand, you just have to add the arugment -h or --help to display command informations with examples.

```bash
wo site --help
```

---

### Get the MySQL root password

MySQL root password is stored in the file `/etc/mysql/conf.d/my.cnf`

### Display MySQL user and password of a site

You can use the command:

```bash
wo site info site.tld
```

---

### Access WordOps backend

WordOps backend is available on port 22222, you can access it with the server IP, hostname or with a domain pointed to the server IP:

```bash
# with server IP
https://YOUR.SERVER.IP:22222

# with server hostname
https://server.site.tld:22222

# with a domain hosted on the server
https://site.tld:22222
```

### Change WordOps backend username and password

You can use the command:

```bash
wo secure --auth
```

---

### Renew a Let's Encrypt SSL Certificates with WordOps

Previously with EasyEngine v3, Let's Encrypt certificates were renewed by running the command `ee site update --le=renew --all` with a cronjob.

You may have noticed the command `site update --le=renew` still exist in WordOps, but you shouln't need it because WordOps use the awesome acme client acme.sh to issue and handle Let's Encrypt SSL certificates. All certificates are **automatically renewed every 60 days** by acme.sh using a cronjob.

However, if you really need to renew your certificates, you can directly use acme.sh to renew all certificates with the following command:

```bash
acme.sh --renew-all --ecc
```
