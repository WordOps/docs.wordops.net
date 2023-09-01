# Define MariaDB and default PHP version

Wordops provide the ability to manually set the MariaDB version you want to install on your server. It support MariaDB from 10.4 to 10.11.

You can also define the default PHP version to install and to use when you create a site without an argument like `--php81`.

Both configurations are available in `/etc/wo/wo.conf`. On a fresh WordOps install, this file will set MariaDB version to the latest LTS release and PHP version to the current supported PHP release.

## Define MariaDB version

### Before installing Mysql stack

On a fresh WordOps install, you can define the MariaDB version before running `wo stack install` or before creating a site requiring a database.

To do so, you just have to open `/etc/wo/wo.conf` with your favorite text editor.

```shell
sudo nano /etc/wo/wo.conf
```

At the bottom of the file, you will find the following block :

```shell
[mariadb]

### Default MariaDB release
release = 10.11
```

To define MariaDB version, just edit the release number.

WordOps support MariaDB version from `10.4` up to `10.11`.

### To upgrade MariaDB

WordOps give you the ability to upgrade MariaDB with the command `wo stack migrate --mariadb`.
You can define the MariaDB version you want to upgrade to the same way than the exemple above.

!!! warning

    It's not possible to downgrade MariaDB, so before upgrading MariaDB, please make sure all your apps are compatible with the release you want to install.


## Define PHP version

On a fresh install as well as on an existant server, you can at anytime set the default PHP version to use when you create new sites.

To do so, you just have to open `/etc/wo/wo.conf` with your favorite text editor.

```shell
sudo nano /etc/wo/wo.conf
```

At the bottom of the file, you will find the following block :

```shell
[php]

### Default PHP version
version = 8.1
```

If you want another PHP version than the one set in this file, just edit the version number.

!!! warning

    Please make sure WordOps support the php version you are going to use.