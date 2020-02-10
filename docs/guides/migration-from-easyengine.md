# Migration from EasyEngine v3

## Running WordOps install script

The first step to migrate from EasyEngine to WordOps is to run WordOps install script with the command:

```bash
wget -qO wo wops.cc && sudo bash wo
```

!!! info
    Before installing WordOps, the install script will backup all previous EasyEngine configurations. You will find them after the installation in `/var/lib/wo-backup`.

It will also create all new Nginx configurations before syncing the old nginx directory with the new one. This way, if you have added custom Nginx configuration, you will find them at the same place than before the migration.

## Post installation steps

After installing WordOps, if all your sites are still working properly, you can start using WordOps the same way as EasyEngine. For sites previously created with EasyEngine, you will have to change some settings in their configuration to use WordOps new configurations. This can be done with the command `wo site update` or by editing manually their configuration with the command `wo site edit`.

!!! warning
    If some sites are still using php5.6 or php7.0 and are not compatible with newer PHP versions, do not change their vhost configuration. WordOps minimum and default PHP version is PHP 7.2. Additionally, sites previously created with `--w3tc`  will have to use another cache option as we deprecated this stack.

### Updating site configuration

You have the choice between two methods to update your site configuration:

- With the command `wo site update` (recommended)

- Manually with the command `wo site edit`

#### Using the command `wo site update`

The easiest way to update your site with the new WordOps configurations is to use the command:

```bash
wo site update site.tld <options>
```

To update your sites configuration, you can enable PHP 7.3 on your site with the argument `--php73` and then disable it with the argument `--php72` to use PHP 7.2.
This will regenerate your site Nginx vhost and apply the new configuration.

**Example**:

```bash
# enable PHP 7.3 to regenerate site configuration
wo site update site.tld --php73
# disable PHP 7.3 to use PHP 7.2 (optional)
wo site update site.tld --php72
```

#### Manually editing site configuration

You can edit sites configuration with the command:

```bash
wo site edit site.tld
```

!!! info

    You will be prompted to choose a text editor, if you are new to linux, we recommend you to choose nano.

In Nginx vhost configuration, you will find several lines beginning with `include`.

To use the new WordOps configuration, you just have to replace the path of the configuration set after `include`.  For example `include common/locations.conf;` has to be replaced by `include common/locations-wo.conf;`.

!!! warning

    Make sure to not remove the `;` at the end of the line when updating Nginx configuration.

For all WordPress related configuration files like `wpsc.conf` or `wpfc-php7.conf`, new configurations files are just named `wpsc-php72.conf` or `wpfc-php72.conf`.

There are some exceptions, list here:

| **Previous configuration** | **New configuration**    |
| -------------------------- | ------------------------ |
| common/locations.conf      | common/locations-wo.conf |
| common/locations-php7.conf | common/locations-wo.conf |
| common/php.conf            | common/php72.conf        |
| common/php7.conf           | common/php72.conf        |

### Removing previous PHP version

If you do not need php5.6 and php7.0 anymore, you can safely remove them with the following commands:

```bash
# php5.6
apt-get -y autoremove php5.6-fpm php5.6-common --purge

# php7.0
apt-get -y autoremove php7.0-fpm php7.0-common --purge
```

### Upgrading MariaDB to 10.3

!!! Warning
    Before upgrading MariaDB, we strongly recommend you to perform a backup of your MySQL databases.

#### Backup your databases

You can backup your MySQL databases with this simple bash script:

```bash
wget https://git.io/JeGSb -O mysqldump.sh
chmod +x mysqldump.sh
```

Then perform a full backup:

```bash
./mysqldump.sh --full
```

This will backup the whole MySQL server and store the gzipped dump in /var/www/mysqldump

Additionally you can make a copy of the `/var/lib/mysql` directory:

```bash
sudo service mysql stop
sudo cp -rf /var/lib/mysql /var/lib/mysql-bak
sudo service mysql start
```

#### Upgrading MariaDB

At first, you need to remove the current MariaDB-server installed. To do so, use the command:

```bash
sudo apt-get autoremove mariadb-server -y
```

Then you can reinstall the latest MariaDB-server version with WordOps:

```bash
wo stack install --mysql
```
