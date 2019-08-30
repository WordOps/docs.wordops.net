
# From EasyEngine to WordOps

WordOps was forked from EasyEngine v3, with the objective of providing an up-to-date version of EasyEngine v3, stable and ready for production.

## Fundamental changes

- We've deprecated the mail stack. As an alternative, you can take a look at [Mail-in-a-Box](https://github.com/mail-in-a-box/mailinabox), [iRedMail](https://www.iredmail.org/) or [Caesonia](https://github.com/vedetta-com/caesonia). As Roundcube alternative, there is [Rainloop](https://www.rainloop.net/) or [Afterlogic WebMail](https://github.com/afterlogic/webmail-lite-8)
- Support for W3TC is dropped as a security precaution.
- PHP 5.6 has been replaced by PHP 7.2 and PHP 7.0 has been replaced by PHP 7.3.
- Nginx-ee package has been replaced by Nginx-wo (based on Nginx stable v1.16.0 with Brotli support)
- HHVM stack has been removed
- Memcached stack has been removed
- Let's Encrypt stack isn't based on letsencrypt-auto anymore, we use acme.sh to handle SSL certificates

If you are going to migrate from EasyEngine v3, here some important informations:

- Previous PHP upstreams in Nginx will not be overwritted
- PHP 5.6 and PHP 7.0 will not be removed or uninstalled
- Previous Nginx common configurations will not be overwritted