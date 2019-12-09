# Post-install Steps

These are the first steps **after** you install WordOps. If you haven't installed it already, please check the [installation guide](installation-guide.md).

## Enable bash_completion

To enable WordOps commands auto-completion, run the following command after WordOps installation:

```bash
source /etc/bash_completion.d/wo_auto.rc
```

## Installing WordOps stacks (optional)

You can install WordOps main stacks with the following command before creating your first site, or create directly a site and WordOps will install required stacks.

Installing WordOps main stacks

```bash
wo stack install
```

<asciinema-player src="/images/stackinstall.cast" autoplay loop cols="125" rows="30"></asciinema-player>

Here the list of WordOps components installed with the above command:

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
| cheat.sh          | Binary      | Command-line Linux cheatsheet          |
| Sendmail          | APT package | Sendmail MTA                           |

### Packages types

- APT package are Debian packages installed from APT repositories
- Binaries are simple executables (do not use any server resources when you are not running them)
- Web App are PHP based applications

## WordOps backend

After installing Nginx, WordOps will display your login credentials to access to WordOps backend.
You haven't saved them ? Don't worry, you can change them at anytime with the command :

```bash
wo secure --auth
```

You will be prompted for a username and a password. If empty, WordOps will use the default username set during the installation and will generate a random password.

You should now be able to access WordOps backend on `https://YOUR.SERVER.IP:22222` or `https://yourserver.hostname.tld:22222`. You will probably be warned about the SSL certificate, but you can learn how to secure WordOps backend with a valid SSL certificate in the next part.

## Securing WordOps backend

To secure WordOps backend with a valid SSL certificate, you just have to create a basic site with the domain/subdomain of your choice. WordOps will automatically use the first SSL certificate issued to secure the backend.

Example :

```bash
wo site create server.domain.tld -le
```

Then you will be able to access to the backend with : `https://server.domain.tld:22222`

## Enabling UFW Firewall

If you haven't already configured a firewall on your server, you can use WordOps to automatically configure UFW with a minimal rules set for WordOps.

```bash
wo stack install --ufw
```

## Creating an alias for sudo wo

If you want to be able to use directly the command `wo` as non-root user, you can add a bash alias to automatically add `sudo` in front of the command `wo`.

Use the following command to add the alias :

```bash
echo -e "alias wo='sudo -E wo'" >> $HOME/.bashrc
```

Then apply it with `source $HOME/.bashrc`
