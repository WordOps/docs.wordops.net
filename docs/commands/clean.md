# clean

Clean NGINX FastCGI cache, Opcache, Redis Cache

Usage:

```bash
wo clean [options]
```

If options are empty, default is `--fastcgi`.

optional arguments   | description
-------------------- | -------------------------
`--fastcgi`          | clean Nginx fastcgi_cache |
`--redis`            | clean redis cache         |
`--opcache`          | clean opcache             |
`--all`              | clean all cache           |
