# Let's Encrypt DNS API configuration

!!! warning
    This feature is available with WordOps v3.9.6 and onward

WordOps use acme.sh to handle SSL certificates, which supports domain validation using DNS API.
This feature is optional to issue domain and subdomain certificates, but is required to issue wildcard certificates.

## DNS API configuration

WordOps use the Acme client [acme.sh](https://github.com/Neilpang/acme.sh) to handle Let's Encrypt SSL certificates. It support DNS API with the most part of popular DNS providers, including Cloudflare, DigitalOcean, OVH, Amazon Route53, Linode, Gandi and many others.

In this example, we will configure Cloudflare DNS API, but configuration will be pretty similar with other DNS providers.

!!! info
    DNS providers list and configurations are available in [acme.sh wiki](https://github.com/Neilpang/acme.sh/wiki/dnsapi)

### Step 1: get your API credentials

Requirements:

- your Cloudflare account email address
- your Global API Key available in your [Cloudflare profile](https://dash.cloudflare.com/profile)

### Step 2: set your credentials with acme.sh variables

Before issuing your first SSL certificate with DNS API, you have to define your API credentials with the command `export` :

Example for Cloudflare:

```bash
export CF_Key="sdfsdfsdfljlbjkljlkjsdfoiwje"
export CF_Email="xxxx@sss.com"
```

- CF_Key: Cloudflare Global API key available in your [Cloudflare profile](https://dash.cloudflare.com/profile)
- CF_Email: Your Cloudflare account email address

Example with DigitalOcean:

```bash
export DO_API_KEY="75310dc4ca779ac39a19f6355db573b49ce92ae126553ebd61ac3a3ae34834cc"
```

Example with GoDaddy:

```bash
export GD_Key="sdfsdfsdfljlbjkljlkjsdfoiwje"
export GD_Secret="asdfsdafdsfdsfdsfdsfdsafd"
```

!!! info
    DNS providers list and configurations are available in [Acme.sh Wiki](https://github.com/Neilpang/acme.sh/wiki/dnsapi)

### Step 3: issue your certificate

For a new site secured with a wildcard SSL certificates with Cloudflare DNS API

```bash
wo site create site.tld --wp --letsencrypt=wildcard --dns=dns_cf
```

- `--letsencrypt=wildcard`: issue a wildcard certificate `domain.tld` + `*.domain.tld`
- `--dns=dns_cf`: enable DNS API mode with Cloudflare.

For an existant secured with a simple SSL certificate (site + www.site.tld) with DigitalOcean DNS API

```bash
wo site update site.tld -le --dns=dns_do
```

- `-le`: issue a certificate for `domain.tld` + `www.domain.tld`
- `--dns=dns_do`: enable DNS API mode with DigitalOcean

## Informations

- You can also use DNS API to issue domain and subdomain certificates.
- `--dns=dns_cf` define the DNS provider to use. With DigitalOcean, it would be `--dns=dns_do`
- After issuing a first certificate using DNS API, your API credentials will be saved in `/etc/letsencrypt/config/account.conf`. You do not need to define them anymore.
