# How to ... ?

## General WordOps usage

#### Get a list of WordOps commands

To get the list of WordOps commands, you can use the command :

```bash
wo
```

Then for any subcommand, you just have to add the arugment -h or --help to display command informations with examples.

```bash
wo site --help
```

#### Get the MySQL root password

MySQL root password is stored in the file `/etc/mysql/conf.d/my.cnf`

#### Display MySQL user and password of a site

You can use the command :

```bash
wo site info site.tld
```

#### Access WordOps backend

WordOps backend is available on port 22222, you can access it with the server IP, hostname or with a domain pointed to the server IP :

```bash
# with server IP
https://YOUR.SERVER.IP:22222

# with server hostname
https://server.site.tld:22222

# with a domain hosted on the server
https://site.tld:22222
```

#### Change WordOps backend username and password

You can use the command :

```bash
wo secure --auth
```

#### Customize WordPress installation locale

You can customize WordPress installation locale by creating the configuration file `~/.wp-cli/config.yml`

```bash
nano ~/.wp-cli/config.yml
```

And by adding the following content inside (just replace en_US by your locale) :

```yaml
core download:
  locale: en_US
```

For example, to install WordPress in French, the file `~/.wp-cli/config.yml` should look like :

```yaml
core download:
  locale: fr_FR
```