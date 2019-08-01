# Troubleshooting

## Common issues

### The command `wo update` failed

This is a known issue with WordOps v3.9.6 which has been fixed with the maintenance release v3.9.6.1.
As a workaround you can either use the command `wo update --beta` or run again the install command :

```bash
wget -qO wo wops.cc && sudo bash wo
```

---

### WordOps failed to issue SSL certificate

At first, make sure your domain is pointed to your server IP :

- www.site.tld + site.tld if you use the flag `-le` or `--letsencrypt`
- sub.site.tld if you use the flag `-le=subdomain` or `--letsencrypt=subdomain`

Then if you need to cleanup the previous SSL certificate, you can use the following command to remove existant certificates and keys, as well as other Nginx configurations for your domain :

```bash
wo site update site.tld --letsencrypt=clean
```

### Nginx CPU usage is very high

This issue seems to be related to brotli but, but even after investigation, we haven't be able to find the cause of this issue yet.

You can disable brotli compression by running the following command :

```bash
sudo sed -i 's/brotli on;/brotli off;/' /etc/nginx/nginx.conf
sudo sed -i 's/brotli_static on;/brotli_static off;/' /etc/nginx/nginx.conf
sudo nginx -t && sudo service nginx restart
```

### When I update a page, changes are not applied on the site

If you are using Nginx fastcgi_cache, please make sure :

- Nginx-helper plugin is enabled
- the option "purge cache" is enabled in Settings > Nginx-Helper
- the caching method is defined on Nginx Fastcgi cache

If you are using Redis-cache, please make sure :

- Nginx-helper plugin is enabled
- the option "purge cache" is enabled in Settings > Nginx-Helper
- the caching method is defined on Redis Cache
- the prefix defined is `nginx-cache:`