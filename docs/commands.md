# WordOps commands

## Top level commands

| command | feature | example |
|-|---------|-|
| [site](#site) | create, delete, edit sites | `wo site create site.tld --wp` |
| [stack](#stack) | install/remove WordOps server stacks | `wo stack install --nginx` |
| [debug](#debug) | commands to do server level debugging | `wo debug site.tld --php` |
| [clean](#clean) | clean Wordops cache backend | `wo clean --fastcgi` |
| [info](#info) | display server stack informations | `wo info --nginx` |
| [log](#log) | perform operation on logs | `wo log show --nginx` |
| [secure](#secure) | manage WordOps backend authentification | `wo secure --auth` |
| [maintenance](#maintenance) | perform server package updates | `wo maintenance`
| [update](#update) | update WordOps | `wo update` |

## Commands

### site

#### create


###### HTML Website

To create simple html website use this command.

```bash
wo site create example.com --html
```

###### PHP Website

To create simple php website with no database use this command.

```bash
wo site create example.com --php
```

###### PHP+MySQL Website

To create simple php website with database use this command.

```bash
wo site create example.com --mysql
```

NOTE: You can find MySQL database details in ee-config.php file.

###### Proxy site

To create site with Proxy configuration you can use --proxy during site creation

```bash
wo site create example.com --proxy=host[:port]
```

Here port is optional and default value is 80.

For example,

```bash
wo site create example.com --proxy=1.2.3.4
```

This will create proxy site example.com with proxy destination as 1.2.3.4

##### WordPress Site

Following are the WordPress website types you can create website based on Cache Mechanism

WordPress type (Single/Multisite)

###### Standard WordPress Sites

To create Standard/Single WordPress site use following command.

```bash
wo site create example.com --wp # install wordpress without any page caching
wo site create example.com --w3tc # install wordpress with w3-total-cache plugin
wo site create example.com --wpsc # install wordpress with whisp-super-cache plugin
wo site create example.com --wpfc # install wordpress + nginx fastcgi_cache
wo site create example.com --wpredis # install wordpress + nginx redis_cache
```

###### WordPress Multisite with subdirectory

To create WordPress Multisite with subdirectory setup use from following command.

```bash
wo site create example.com --wpsubdir # install wpmu-subdirectory without any page caching
wo site create example.com --wpsubdir --w3tc # install wpmu-subdirectory with w3-total-cache plugin
wo site create example.com --wpsubdir --wpsc # install wpmu-subdirectory with wp-super-cache plugin
wo site create example.com --wpsubdir --wpfc # install wpmu-subdirectory + nginx fastcgi_cache
wo site create example.com --wpsubdir --wpredis # install wpmu-subdirectory + nginx redis_cache
```

WordPress Multisite with subdomain To create WordPress Multisite with subdomain setup use from following command.

```bash
wo site create example.com --wpsubdom # install wpmu-subdomain without any page caching
wo site create example.com --wpsubdom --w3tc # install wpmu-subdomain with w3-total-cache plugin
wo site create example.com --wpsubdom --wpsc # install wpmu-subdomain with wp-super-cache plugin
wo site create example.com --wpsubdom --wpfc # install wpmu-subdomain + nginx fastcgi_cache
wo site create example.com --wpsubdom --wpredis # install wpmu-subdomain + nginx redis_cache
```

##### WordPress Additional settings

Define WordPress administrator user To define wordpress administrator user during site creation use

```bash
wo site create example.com --user=admin
```

This will create admin as administrator user in wordpress during installation. If not defined it will take git user name.

Define WordPress administrator password To define wordpress administrator password during site creation use

```bash
wo site create example.com --pass=password
```

This will set defined password as administrator password. If not defined it will generate random pasword for administrator. If you have special characters, you can quote them using single quotes like this Ã¢â‚¬"

--pass='my$secret&' Define WordPress administrator email To define wordpress administrator email during site creation use

```bash
wo site create example.com --email=ee@example.com
```

This will set defined email as administrator email. If not defined it will set git email as administrator email.

##### Additional features

WordOps supports Let's Encrypt out of the box.

```bash
wo site create example.com --letsencrypt
```

You can add --letsencrypt to any other flag.

###### PHP 7.3

To create site with PHP 7.3 you can use --php73 during site creation

For example, you can create WordPress site running on PHP 7.3 using following command:

```bash
wo site create example.com --wp --php73
```

To create simple php(with v7.0) website with no database use this command.

```bash
wo site create example.com --php73
```

###### Let's Encrypt

WordOps supports Let's Encrypt out of the box.

```bash
wo site create example.com --letsencrypt
```

You can add --letsencrypt to any other flag.

--------------------------------------------------------------------------------

#### delete

To delete site created with EasyEngine (ee) use

```bash
ee site delete example.com</code>
```

###### Delete website without prompt

```bash
ee site delete example.com --no-prompt</code>
```

###### Delete website webroot only

```bash
ee site delete example.com --files</code>
```

###### Delete website database only

```bash
ee site delete example.com --db</code>
```
### stack

#### Sets of packages

##### Web

This will install Nginx, PHP 7.2, MariaDB & additional tools available on port 22222

```bash
wo stack install
```

or

```bash
wo stack install web
```

##### Admin tools

```bash
wo stack install --admin
```

#### Individual packages

##### Nginx

```bash
wo stack install --nginx
```

##### PHP 7.2

```bash
wo stack install --php
```

##### MariaDB (MySQL)

```bash
wo stack install --mysql
```

##### Adminer

```bash
wo stack install --adminer
```

##### PHPMyAdmin

```bash
wo stack install --phpmyadmin
```

### debug

### clean

### info

### log

### secure

### maintenance

### update