# Migration from EasyEngine v3

## Running WordOps install script

The first step to migrate from EasyEngine to WordOps is to run WordOps install script with the command :

```bash
wget -qO wo wops.cc && sudo bash wo
```

!!! info
    Before installing WordOps, the install script will backup all previous EasyEngine configurations. You will find them after the installation in `/var/lib/wo-backup`.

It will also create all new Nginx configurations before syncing the old nginx directory with the new one. This way, if you have added custom Nginx configuration, you will find them at the same place than before the migration. 



## Post installation steps

After installing WordOps, if all your sites are still working properly, you can start using WordOps the same way than EasyEngine. For sites previously created with EasyEngine, you will have to changes some settings in their configuration to use WordOps new configurations. This can be done with the command `wo site update` or by editing manually their configuration with the command `wo site edit`.

!!! warning

    If some sites are still using php5.6 or php7.0 and are not compatible with newer PHP versions, do not change their vhost configuration. WordOps minimum and default PHP version is PHP 7.2. Additionally sites previously created with `--w3tc`  will have to use another cache option as we deprecated this stack. 

### Updating site configuration

You have the choice between two method to update your site configuration : 

- With the command `wo site update` (recommended)

- Manually with the command `wo site edit`

#### Using the command `wo site update`

The easiest way to update your site with the new WordOps configurations is to use the command : 

```bash
wo site update site.tld <options>
```

##### WordPress sites

To update a WordPress site, you just have to switch to another cache backend before switching back the previous cache backend used. For example, for a site created with the argument `--wp`, you just have to use another option like `--wpfc` and to switch back to `--wp`. 



**Example** : for a site created with `--wpsc`.

```bash
# switch to another cache backend to update nginx configuration
wo site update site.tld --wp
# switch back to the cache option previously used
wo site update site.tld --wpsc
```

!!! info

    It's not possible to update a site created with the argument `--wp` just by running `wo site update site.tld --wp` because like EasyEngine, WordOps verify previous type and the new one to make sure it's not the same.

##### Non WordPress sites

For non WordPress sites, the method is pretty similar to the one used for WordPress sites. You can enable PHP 7.3 on your site with the argument `--php73` before disabling it with the argument `--php73=off`.

This will regenerate your site configuration with the new WordOps configurations.

***Example** : for a basic site  created with `--mysql`

```bash
# enable PHP 7.3 to regenerate site configuration
wo site update site.tld --php73
# disable PHP 7.3 to use PHP 7.2 (optional)
wo site update site.tld --php73=off
```

#### Manually editing site configuration

You can edit sites configuration with the command : 

```bash
wo site edit site.tld
```

!!! info

    You will be prompt to choose a text editor, if you are new to linux, we recommend you to choose nano.



In Nginx vhost configuration, you will find several lines beginning with `include`. 

To use new WordOps configuration, you just have to replace the path of the configuration set after `include`.  For example `include common/locations.conf;` have to be replaced by `include common/locations-wo.conf;`.

!!! warning

    Make sure to not remove the `;` at the end of the line when updating Nginx configuration.



For all WordPress related configuration files like `wpsc.conf` or `wpfc-php7.conf`, new configurations files are just named `wpsc-php72.conf` or `wpfc-php72.conf`.

There are some exceptions, list here : 

| **Previous configuration** | **New configuration**    |
| -------------------------- | ------------------------ |
| common/locations.conf      | common/locations-wo.conf |
| common/locations-php7.conf | common/locations-wo.conf |
| common/php.conf            | common/php72.conf        |
| common/php7.conf           | common/php72.conf        |


