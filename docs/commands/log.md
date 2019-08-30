# log

Perform operations on Nginx, PHP and MySQL log files

Usage:

```bash
wo log [<site_name>] [options]
```

subcommand      | description
--------------- | --------------------------------
[gzip](#gzip)   | GZip Nginx, PHP, MySQL log file
[mail](#mail)   | Mail Nginx, PHP, MySQL log file
[show](#log-show)   | Show Nginx, PHP, MySQL log file
[reset](#reset) | Reset Nginx, PHP, MySQL log file

## log show

Show Nginx, PHP, MySQL log file

Usage:

```bash
wo log show [<site_name>] [options]</site_name>
```

optional arguments   | description
-------------------- | --------------------------------------
`--nginx`            | Show Nginx Error logs file             |
`--php`              | Show PHP Error logs file               |
`--mysql`            | Show MySQL logs file                   |
`--wp`               | Show Site specific WordPress logs file |
