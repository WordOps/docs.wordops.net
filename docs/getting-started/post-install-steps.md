# Post-install Steps

These are the first steps **after** you install WordOps. If you haven't installed it already, please check the [installation guide](installation-guide.md).

## Enable bash_completion

To enable WordOps commands auto-completion, run the following command after WordOps installation :

```bash
source /etc/bash_completion.d/wo_auto.rc
```

## Installing WordOps stacks (optional)

Before creating your first site with WordOps, you can install WordOps main stacks with the command

```bash
wo stack install
```

<video align="center" src="/images/wo-stack.webm" width="760" autoplay loop></video>

Here the list of WordOps components installed with the above

Component         | Description
----------------- | --------------------------------------
Nginx             | WordOps web server                     |
PHP 7.2           | PHP7.2-FPM                             |
MariaDB 10.3      | Open-source version of MySQL           |
WP-CLI            | The WordPress command-line tool
Composer          | PHP packages manager                   |
MySQLTuner        | Command-line tool to tune MySQL        |
phpMyAdmin        | MySQL server web interface             |
Adminer           | lightweight phpMyAdmin alternative     |
OpcacheGUI        | web interface for Opcache monitoring   |
Netdata           | Monitoring suite                       |
Anemometer        | MySQL Slow Query Monitor               |
WordOps dashboard | Bootstrap template for WordOps backend |
eXtplorer         | Web File manager                       |
Fail2ban          | Authentication bruteforce protection   |
