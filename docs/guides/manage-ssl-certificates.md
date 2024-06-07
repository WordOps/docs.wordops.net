# Manage Let's Encrypt SSL certificates

In this guide, we will explain how to issue a Let's Encrypt SSL certificate to secure your site and the different options available.

To issue a SSL certificate with WordOps, you can use the following arguments with the commands:

-   `wo site create`
-   `wo site update`

| options                     | description                                                                       |
| --------------------------- | --------------------------------------------------------------------------------- |
| `--letsencrypt` / `-le`     | issue a SSL certificate for domain or subdomain                                   |
| `--letsencrypt=wildcard`    | issue a wildcard SSL certificate: **domain.tld + \*.domain.tld**                  |
| `--dns` / `--dns=<dns_api>` | use DNS API validation for Acme challenge. **required for wildcard certificates** |

`-le` is an alias for `--letsencrypt`. You can use this alias with all letsencrypt commands.

For example, `--letsencrypt=wildcard` is the same than `-le=wildcard`

## Issuing a certificate

### Webroot mode

By default WordOps use the Webroot mode to validate the domain. This mode doesn't require any additional configuration.

#### domain + www.domain.tld

To create a new site:

```bash
wo site create site.tld --wp -le
```

To secure an existant site:

```bash
wo site update site.tld -le
```

#### sub-domain

To create a new site:

```bash
wo site create sub.site.tld --wp -le
```

To secure an existant site:

```bash
wo site update sub.site.tld -le
```

### DNS API mode

!!! warning

<!-- prettier-ignore -->
    Read first our guide about [DNS API configuration](/how-to/configure-letsencrypt-dns-api-validation/)

<!-- prettier-ignore-end -->

#### domain or subdomain

To create a new site with Cloudflare DNS API:

```bash
wo site create site.tld --wp -le --dns=dns_cf
```

To secure an existant site with DigitalOcean DNS API:

```bash
wo site update sub.site.tld -le --dns=dns_dgon
```

#### wildcard

To create a new site with Cloudflare DNS API:

```bash
wo site create site.tld --wp --letsencrypt=wildcard --dns=dns_cf
```

To secure an existant site with DigitalOcean DNS API:

```bash
wo site update site.tld -le=wildcard --dns=dns_dgon
```
