# How to get an A+ Grade on ssllabs with WordOps

This tutorial describe how to get the best score with the SSL   your site

## Step 1) Issue an ssl certificate with WordOps and enable HSTS

### For a new site

```bash
wo site create site.tld --wp -le --hsts
```

### For an existant site

```bash
wo site update site.tld -le --hsts
```

### Enabling HSTS on a site already secured with Let's Encrypt

```bash
wo site update site.tld --hsts
```

## Step 2)