# How to secure WordOps backend with Let's Encrypt SSL certificate

From the release v3.9.8.1 and onward, WordOps will automatically secure the backend on port 22222 with the first SSL certificate issued on the server. So you just have to create basic site with the arguments `--letsencrypt` or `-le` to secure the backend.

## Using another certificate

### Secure WordOps backend with the same certificate than another site

If you already have a site secured with Let's Encrypt, you just have to copy the `ssl.conf` file stored in `/var/www/site.tld/conf/nginx`.

```bash
DOMAIN_NAME=site.ltd
sudo grep "ssl_" /var/www/${DOMAIN_NAME}/conf/nginx/ssl.conf > /var/www/22222/conf/nginx/ssl.conf
```

Then reload Nginx:

```bash
wo stack restart --nginx
```

You should now be able to access to WordOps backend on `https://site.tld:22222`

### Issue a new certificate to secure WordOps backend

If you prefer to issue manually a new Let's Encrypt SSL certificate, here the steps to follow:

Set your domain or subdomain as a variable:

```bash
DOMAIN_NAME=backend.site.ltd
```

Issue the certificate

```bash
acme.sh --issue -d $DOMAIN_NAME -k ec-384 -w /var/www/html
```

If the certificate as issued successfully, create a directory to store the certificate

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
--reloadcmd "nginx -t && systemctl restart nginx.service"
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
wo stack restart --nginx
```
