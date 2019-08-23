# How to get an A+ Grade on ssllabs with WordOps

This tutorial describe how to get the best SSL grade on ssllabs.com. To get an A+, it require to enable HSTS (HTTP Strict Transport Security). HSTS allows web servers to declare that web browsers should only interact with it using HTTPS connections and never via the insecure HTTP protocol.

!!! Warning
    Make sure your site/domain and subdomains will never need to use HTTP again, because after accessing a single time to your site with HSTS enabled, your web browser will not allow you to access it over http if you remove the SSL certificate for example.

## Issue an ssl certificate with WordOps and enable HSTS

### For a new site

For a domain

```bash
wo site create site.tld --wp -le --hsts
```

For a subdomain

```bash
wo site create sub.site.ltd --wp -le=subdomain --hsts
```

For a multisite

```bash
wo site create site.tld --wpsubdom -le=wildcard --hsts
```

### For an existant site without SSL

For a domain

```bash
wo site update site.tld -le --hsts
```

For a subdomain

```bash
wo site update sub.site.ltd -le=subdomain --hsts
```

For a multisite

```bash
wo site update site.tld -le=wildcard --hsts
```

### For an existant site already secured with Let's Encrypt

For a domain

```bash
wo site update site.tld --hsts
```

For a subdomain

```bash
wo site update sub.site.ltd --hsts
```

For a multisite

```bash
wo site update site.tld --hsts
```

Congratulations, you can now check your grade on https://www.ssllabs.com/ssltest/

### Switching HSTS off

It's not recommended to disable HSTS because web browser will store the HSTS directive for a long time (6 months) and will not allow access over HTTP even after disabling HSTS on the server. However, if you absolutely need to disable HSTS, you can use the following command :

```bash
wo site update site.tld --hsts=off
```

## Hardening HSTS

You can increase even more your site security by enabling HSTS preloading on your domain. It's the same than HSTS, but this time your domain will be directly added into the hstspreload.org list and web browsers will enable HSTS even without accessing to your site.

This can be done on https://hstspreload.org
