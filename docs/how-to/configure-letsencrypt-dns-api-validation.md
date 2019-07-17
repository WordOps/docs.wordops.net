# Let's Encrypt DNS API configuration

!!! warning
    This feature is available with WordOps v3.9.6 and onward

WordOps use acme.sh to handle SSL certificates, which supports domain validation using DNS API.
This feature is optional to issue domain and subdomain certificates, but is required to issue wildcard certificates.

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