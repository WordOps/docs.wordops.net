# F.A.Q

## What is WordOps ?

WordOps is a command line tool which provide the ability to install WordPress on an optimized LEMP stack (Nginx, PHP, MySQL) with simple command like `wo site create site.tld --wp`.

## Which operating systems are supported by WordOps ?

WordOps can be installed on Ubuntu LTS (Long Term Service) releases (16.04 & 18.04) as well as on Debian 8 (Jessie) or Debian 9 (stretch)
Support for other linux distribution isn't planned.

## How to get a list of the WordOps commands ?

To get the list of WordOps commands, you just have to use the command :

```bash
wo
```

It's the same with subcommands :

```bash
wo site
```

## What is the best caching solution for WordPress ?

There is no "best solution", because there are benefits/disadvantage for each caching solution and it depend on your usage.

Here some informations :

- fastcgi_cache (`--wpfc`) is the simplest solution, because it do not rely on any plugin excepted nginx_helper used to purge cache after content updates.
- redis-cache (`--wpredis`) is a powerful solution which support multi-server setup and it provide full-page cache in redis via Nginx + object-cache via Redis-Object-Cache plugin (also used to purge cache)
- wp-super-cache (`--wpsc`) is a basic solution based on a plugin which create and serve static html files.

## Why gzip compression is disabled by default ?

We disabled gzip compression by default due to gzip related security issues when using TLS connection. More informations here [BREACH CVE](https://en.wikipedia.org/wiki/BREACH).
We replaced gzip by brotli, which provide better performance and compression than gzip.
