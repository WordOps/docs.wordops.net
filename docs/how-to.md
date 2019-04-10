# How to ?

## General WordOps usage

#### How to get a list of WordOps commands ?

To get the list of WordOps commands, you can use the command :

```bash
wo
```

Then for any subcommand, you just have to add the arugment -h or --help to display command informations with examples.

```bash
wo site --help
```

#### How to get the MySQL root password ?

MySQL root password is stored in the file `/etc/mysql/conf.d/my.cnf`

#### How to get MySQL user and password of a site ?

You can use the command :

```bash
wo site info site.tld
```

#### How to access WordOps backend ?

WordOps backend is available on port 22222, you can access it with the server IP, hostname or with a domain pointed to the server IP :

```bash
# with server IP
https://YOUR.SERVER.IP:22222

# with server hostname
https://server.site.tld:22222

# with a domain hosted on the server
https://site.tld:22222
```

#### How to change WordOps backend on port 22222 username and password ?

You can use the command :

```bash
wo secure --auth
```
