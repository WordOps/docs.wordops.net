# How to ?

## General WordOps usage

### How to get a list of WordOps commands ?

To get the list of WordOps commands, you can use the command :

```bash
wo
```

Then for any subcommand, you just have to add the arugment -h or --help to display command informations with examples.

```bash
wo site --help
```

### How to get the MySQL root password ?

MySQL root password is stored in the file `/etc/mysql/conf.d/my.cnf`

### How to change WordOps backend on port 22222 username and password ?

You can use the command :

```bash
wo secure --auth
```
