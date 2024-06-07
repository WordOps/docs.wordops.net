# F.A.Q

## General

### What is WordOps ?

WordOps is a command line tool which ease server administration and WordPress deployment by providing the ability to setup an optimized LEMP stack (Nginx, PHP, MySQL) with simple command like `wo stack install --nginx`.

### What are WordOps main features ?

WordOps not only installs and configures the packages needed to deploy a site (Nginx, PHP, MariaDB) but it also takes care of creating Nginx vhosts and the database, installing WordPress and even get a Let's Encrypt SSL certificate, all in one command line. It support multiple cache backend for WordPress, including Nginx fastcgi_cache, Redis cache (full-page cache + object cache) or wp-super-cache, based on a highly optimized Nginx configuration and an hardened security with strict location directives.

### Which operating systems are supported by WordOps ?

WordOps can be installed on Ubuntu LTS (Long Term Service) releases (18.04, 20.04 & 22.04). We do not officialy support Debian distribution (Debian 10/11 & Raspbian 10/11) because we are not able to run our continuous integration on it.
Support for other linux distribution isn't planned.

## Technical

### Which version of PHP does WordOps support ?

WordOps support PHP 8.2 (default) 7.4, 8.1 & 8.3

### What is the best caching solution for WordPress ?

There is no "best solution", because there are benefits/disadvantage for each caching solution and it depend on your usage.

Here some informations:

| Cache backend  | command argument | description                                                                                                                                                  |
| -------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| fastcgi_cache  | `--wpfc`         | the simplest solution, because it do not rely on any plugin excepted nginx_helper used to purge cache after content updates                                  |
| redis-cache    | `--wpredis`      | powerful solution which support multi-server setup and it provide full-page cache in redis via Nginx + object-cache via Redis-Object-Cache plugin (optional) |
| wp-super-cache | `--wpsc`         | basic solution based on a plugin which create and serve static html files.                                                                                   |
| wp-rocket      | `--wprocket`     | solution based on a popular premium plugin with several additional features, compatible with Woocommerce and the most part of plugins                        |
| cache-enabler  | `--wpce`         | solution based on an open-source plugin from keycdn                                                                                                          |

### How to access to WordOps Dashboard ?

WordOps dashboard is available on `https://YOUR.SERVER.IP:22222` or `https://YOUR.SERVER.HOSTNAME:22222`

### What is the user/password of the web filemanager ?

By default, user is admin and password too. After you logged in for the first time, you will have to change this password

### Why do I get warning from my web browser when opening WordOps backend ?

At the moment, WordOps backend is secured with a self-signed SSL certificate, which provide the same level of encryption than any other certificate but do not come from a certificate authority. Your Web browser only warn you about the fact that the certificate wasn't issued by a trusted certificate authority. We are already working on adding the ability to secure WordOps backend with a letsencrypt SSL certificate.

### Does Nginx-wo support TLSv1.3 ?

Yes, since the release v3.9.5.4, our Nginx package support TLSv1.3.

### Is WordOps Let's Encrypt stack compatible with Cloudflare CDN ?

WordOps Let's Encrypt stack is fully compatible with Cloudflare CDN, and you can use Cloudflare DNS API to issue your certificates even if the domain is not pointed to your server IP.

### How to uninstall WordOps ?

If you need/want to uninstall WordOps, you can use the following commands:

!!! warning

<!-- prettier-ignore -->
    Make a backup of your databases before purging wordops packages

<!-- prettier-ignore-end -->

```bash
# purge wordops packages (nginx, mysql, php etc..)
wo stack purge --all

# uninstall wordops
wget -qO wo wops.cc && sudo bash wo --purge
```
