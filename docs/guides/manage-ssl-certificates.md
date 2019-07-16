# Manage Let's Encrypt SSL certificates

In this guide, we will explain how to issue a Let's Encrypt SSL certificate to secure your site and the different options available.

To issue a SSL certificate with WordOps, you can use the following arguments with the commands :

- `wo site create`
- `wo site update`

options        | description
--------------------------|----------------------------------------------------------------------------------
`-letsencrypt` / `-le`    | issue a SSL certificate : **domain.tld + www.domain.tld**
`--letsencrypt=subdomain` | issue a SSL certificate for a subdomain : **sub.domain.tld**
`--letsencrypt=wildcard`  | issue a wildcard SSL certificate : **domain.tld + \*.domain.tld**
`--dns=<dns_api>`         | use DNS API validation for Acme challenge. **required for wildcard certificates**

`-le` is an alias for `--letsencrypt`. You can use this alias with all letsencrypt commands.

For example, `--letsencrypt=wildcard` is the same than `-le=wildcard`

## Issuing a certificate

### Webroot mode

By default WordOps use the Webroot mode to validate the domain. This mode doesn't require any additional configuration.

#### domain + www.domain.tld

To create a new site :

```bash
wo site create site.tld --wp -le
```

To secure an existant site :

```bash
wo site update site.tld -le
```

#### sub-domain

To create a new site :

```bash
wo site create sub.site.tld --wp --letsencrypt=subdomain
```

To secure an existant site :

```bash
wo site update sub.site.tld --letsencrypt=subdomain
```

### DNS API mode

!!! warning
    This feature is available with WordOps v3.9.6 and onward

WordOps also support domain validation using DNS API. This is optional to issue domain and subdomain certificates, but it's required to issue wildcard certificates.

#### DNS API configuration

WordOps use the Acme client [acme.sh](https://github.com/Neilpang/acme.sh) to handle Let's Encrypt SSL certificates. It support DNS API with the most part of popular DNS providers, including Cloudflare, DigitalOcean, OVH, Amazon Route53, Linode, Gandi and many others.

In this example, we will configure Cloudflare DNS API, but configuration will be pretty similar with other DNS providers.

!!! info
    DNS providers list and configurations are available in [acme.sh wiki](https://github.com/Neilpang/acme.sh/wiki/dnsapi)

#### Step 1 : get your API credentials

Requirements :

- your Cloudflare account email address
- your Global API Key available in your [Cloudflare profile](https://dash.cloudflare.com/profile)

#### Step 2 : set your credentials with acme.sh variables

Before issuing your first SSL certificate with DNS API, you have to define your API credentials with the command `export`  :

```bash
export CF_Key="sdfsdfsdfljlbjkljlkjsdfoiwje"
export CF_Email="xxxx@sss.com"
```

Where **CF_Key** is your Cloudflare API Key, and **CF_Email** your Cloudflare account email address.

#### Step 3 : issue your certificate with WordOps

To create a new site :

```bash
wo site create site.tld --wp --letsencrypt=wildcard --dns=dns_cf
```

To secure an existant site :

```bash
wo site update site.tld --letsencrypt=wildcard --dns=dns_cf
```

Informations :

- You can also use DNS API to issue domain and subdomain certificates.
- `--dns=dns_cf` define the DNS provider to use. With DigitalOcean, it would be `--dns=dns_do`
- After issuing a first certificate using DNS API, your API credentials will be saved in `/etc/letsencrypt/config/account.conf`. You do not need to define them anymore.
