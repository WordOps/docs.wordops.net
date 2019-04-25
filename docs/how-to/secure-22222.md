# How to secure WordOps backend with Let's Encrypt SSL certificate

We are currently working on refactoring the Let's Encrypt stack from scratch, to add support for DNS validation, wildcard SSL certificates and to secure WordOps backend automatically.

Those new features are planned for the next WordOps release (v4.0). But we have already make some changes on WordOps backend configuration, and it's already easier to secure the backend available on the port 22222 with Let's Encrypt SSL certificate.

## Secure WordOps backend with the same certificate than another site

If you already have a site secured with Let's Encrypt, you just have to copy the `ssl.conf` file stored in `/var/www/site.tld/conf/nginx`.

```bash
sudo cp -f /var/www/site.tld/conf/nginx/ssl.conf /var/www/22222/conf/nginx/ssl.conf
```

Then reload Nginx :

```bash
sudo service nginx reload
```

You should now be able to access to WordOps backend on `https://site.tld:22222`

## Issue a new certificate to secure WordOps backend

If you prefer to issue manually a new Let's Encrypt SSL certificate, here the steps to follow :

Set your domain or subdomain as a variable :

```bash
DOMAIN_NAME=backend.site.ltd
```

Issue the certificate

```bash
acme.sh --issue -d $DOMAIN_NAME -k ec-384 -w /var/www/html
```

If the certificate was issued successfully, create a directory to store the certificate

```bash
sudo mkdir -p /etc/letsencrypt/live/${DOMAIN_NAME}
```

Install the certificate

```bash
acme.sh --install-cert -d $DOMAIN_NAME --ecc \
--cert-file /etc/letsencrypt/live/$DOMAIN_NAME/cert.pem \
--key-file /etc/letsencrypt/live/$DOMAIN_NAME/key.pem \
--fullchain-file /etc/letsencrypt/live/$DOMAIN_NAME/fullchain.pem \
--ca-file /etc/letsencrypt/live/$DOMAIN_NAME/ca.pem \
--reloadcmd "systemctl restart nginx.service"
```

Create the Nginx configuration

```bash
cat <<EOF >/var/www/22222/conf/nginx/ssl.conf
    ssl_certificate /etc/letsencrypt/live/$DOMAIN_NAME/fullchain.pem;
    ssl_certificate_key     /etc/letsencrypt/live/$DOMAIN_NAME/key.pem;
    ssl_trusted_certificate /etc/letsencrypt/live/$DOMAIN_NAME/ca.pem;
EOF
```

Then reload nginx

```bash
sudo service nginx reload
```