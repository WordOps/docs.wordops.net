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

Here the list of WordOps components installed with the above command

| Packages          | type        | Description                            |
| ----------------- | ----------- | -------------------------------------- |
| Nginx             | APT package | WordOps web server                     |
| PHP 7.2           | APT package | PHP7.2-FPM                             |
| MariaDB 10.3      | APT package | Open-source version of MySQL           |
| WP-CLI            | Binary      | The WordPress command-line tool        |
| Composer          | Binary      | PHP packages manager                   |
| MySQLTuner        | Binary      | Command-line tool to tune MySQL        |
| Fail2ban          | APT package | Authentication bruteforce protection   |
| phpMyAdmin        | Web App     | MySQL server web interface             |
| Adminer           | Web App     | lightweight phpMyAdmin alternative     |
| OpcacheGUI        | Web App     | web interface for Opcache monitoring   |
| Netdata           | Binary      | Monitoring suite                       |
| Anemometer        | Web App     | MySQL Slow Query Monitor               |
| WordOps dashboard | Web App     | Bootstrap template for WordOps backend |
| eXtplorer         | Web App     | Web File manager                       |
| Cheat.sh          | Binary      | Command-line Linux cheatsheet          |

### Packages types

- APT package are debian packages installed from APT repositories
- Binaries are simple executables
- Web App are php based applications
