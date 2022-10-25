
# Common issues

## The command `wo update` failed

If you have any issue when you want to update WordOps, do not hesitate to use the initial install command :

```bash
wget -qO wo wops.cc && sudo bash wo
```

---

## WordOps failed to issue SSL certificate

If you are using DNS API validation :

- Make sure your API credentials has been properly saved by acme.sh in `/etc/letsencrypt/config/account.conf`
- Check acme.sh documentation about DNS API to see if there are changes with your DNS API Provider : https://github.com/Neilpang/acme.sh/wiki/dnsapi

If you are using the default webroot validation :

Make sure your domain is pointing to your server IP as well as `www` alias if it's not a subodmain

If you are behind a load-balancer or a proxy, and need to force WO to issue a certificate even if the domain doesn't resolve your server IP, you can use the flag `--force`

```bash
wo site update site.tld -le --force
```

Then if you need to cleanup the previous SSL certificate, you can use the following command to remove existant certificates and keys, as well as other Nginx configurations for your domain:

```bash
wo site update site.tld --letsencrypt=clean
```

---

## When I update a page, changes are not applied on the site

If you are using Nginx fastcgi_cache, please make sure:

- Nginx-helper plugin is enabled
- the option "purge cache" is enabled in Settings > Nginx-Helper
- the caching method is defined on Nginx Fastcgi cache

If you are using Redis-cache, please make sure:

- Nginx-helper plugin is enabled
- the option "purge cache" is enabled in Settings > Nginx-Helper
- the caching method is defined on Redis Cache
- the prefix defined is `nginx-cache:`

## WordOps commands are not working

If the error output looks like:

```bash
Traceback (most recent call last):
  File "/usr/local/bin/wo", line 6, in <module>
    from pkg_resources import load_entry_point
  File "/usr/lib/python3/dist-packages/pkg_resources/__init__.py", line 3088, in <module>
    @_call_aside
  File "/usr/lib/python3/dist-packages/pkg_resources/__init__.py", line 3072, in _call_aside
    f(*args, **kwargs)
  File "/usr/lib/python3/dist-packages/pkg_resources/__init__.py", line 3101, in _initialize_master_working_set
    working_set = WorkingSet._build_master()
  File "/usr/lib/python3/dist-packages/pkg_resources/__init__.py", line 574, in _build_master
    ws.require(__requires__)
  File "/usr/lib/python3/dist-packages/pkg_resources/__init__.py", line 892, in require
    needed = self.resolve(parse_requirements(requirements))
  File "/usr/lib/python3/dist-packages/pkg_resources/__init__.py", line 778, in resolve
    raise DistributionNotFound(req, requirers)
pkg_resources.DistributionNotFound: The 'wo==3.9.8.2' distribution was not found and is required by the application
```

Just remove the executable `/usr/local/bin/wo` and reinstall WordOps:

```bash
sudo rm -f /usr/local/bin/wo && wget -qO wo wops.cc && sudo bash wo
```

If the issue still persist, open an issue on the GitHub repository.
