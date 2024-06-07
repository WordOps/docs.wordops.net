# site

Performs website specific operations

Usage:

```bash
wo site (command) [options]
```

| subcommand               | description                       |
| ------------------------ | --------------------------------- |
| [create](#site-create)   | Create site with WordOps          |
| [update](#site-update)   | Update site type or configuration |
| [info](#site-info)       | Get site information              |
| [show](#site-show)       | Show site Nginx configuration     |
| [edit](#site-edit)       | Edit site Nginx configuration     |
| [delete](#site-delete)   | Delete site                       |
| [list](#site-list)       | List all sites                    |
| [enable](#site-enable)   | Enable site in Nginx              |
| [disable](#site-disable) | Disable site in Nginx             |
| [cd](#site-cd)           | Move into site webroot directory  |

## site create

<asciinema-player src="/images/wositecreate.cast" autoplay loop cols="125" rows="30"></asciinema-player>

### Usage

```bash
wo site create  [<site_name>] [options]
```

### Basic sites

#### HTML site

To create simple html website use this command.

```bash
wo site create site.tld --html
```

#### PHP site

To create simple php website with no database use this command.

```bash
wo site create site.tld --php
```

#### PHP+MySQL site

To create simple php website with database use this command.

```bash
wo site create site.tld --mysql
```

NOTE: You can find MySQL database details in `/var/www/site.tld/wo-config.php`.

#### Proxy site

To create site with Proxy configuration you can use --proxy during site creation

```bash
wo site create site.tld --proxy=127.0.0.1:3000
```

This will create proxy site site.tld with proxy destination as 127.0.0.1:3000. Port is optional. Default port: 80.

#### Alias site

To create an alias site you can use --alias during site creation

```bash
wo site create site.tld --alias sitetoredirect.tld
```

It will create a nginx vhost for site.tld which redirect to sitetoredirect.tld.

### WordPress

Following are the WordPress website types you can create website based on Cache Mechanism

Standard WordPress site

```bash
wo site create site.tld --wp
```

WordPress site + Nginx fastcgi_cache

```bash
wo site create site.tld --wpfc
```

WordPress site + Redis cache

```bash
wo site create site.tld --wpredis
```

WordPress site + WP-Super-cache

```bash
wo site create site.tld --wpsc
```

WordPress site + WP-Rocket cache

```bash
wo site create site.tld --wprocket
```

WordPress site + Cache enabler

```bash
wo site create site.tld --wpce
```

Enable Ultimate Nginx bad blocker on new site

```bash
wo site create site.tld --ngxblocker
```

#### Cheatsheet

| Cache                     | single site  | multisite w/ subdir     | multisite w/ subdom        |
| ------------------------- | ------------ | ----------------------- | -------------------------- |
| **NO Cache**              | `--wp`       | `--wpsubdir`            | `--wpsubdomain`            |
| **WP Super Cache plugin** | `--wpsc`     | `--wpsubdir --wpsc`     | `--wpsubdomain --wpsc`     |
| **Nginx fastcgi_cache**   | `--wpfc`     | `--wpsubdir --wpfc`     | `--wpsubdomain --wpfc`     |
| **Redis cache**           | `--wpredis`  | `--wpsubdir --wpredis`  | `--wpsubdomain --wpredis`  |
| **WP-Rocket plugin**      | `--wprocket` | `--wpsubdir --wprocket` | `--wpsubdomain --wprocket` |
| **Cache-Enabler plugin**  | `--wpce`     | `--wpsubdir --wpce`     | `--wpsubdomain --wpce`     |

#### Extra settings

##### Define WordPress administrator user

To define WordPress administrator user during site creation use

```bash
wo site create site.tld --user=admin
```

This will create admin as administrator user in WordPress during installation. If not defined it will take git user name.

##### Define WordPress administrator password

To define WordPress administrator password during site creation use

```bash
wo site create site.tld --pass=password
```

This will set defined password as administrator password. If not defined it will generate random pasword for administrator. If you have special characters, you can quote them using single quotes like this:

```bash
--pass='my$secret&'
```

##### Define WordPress administrator email

To define WordPress administrator email during site creation use

```bash
wo site create site.tld --email=wo@site.tld
```

This will set defined email as administrator email. If not defined it will set git email as administrator email.

##### Virtual host only

To create WordPress site and database without installing it, you can use --vhostonly during site creation

For example, you can only create vhost and database without installing WordPress using following command:

```bash
wo site create site.tld --wp --vhostonly
```

### Additional features

#### Let's Encrypt

WordOps supports Let's Encrypt out of the box.

##### Domain

```bash
wo site create site.tld --wp --letsencrypt
```

This command will issue a certificate for site.tld + www.site.tld.

##### Subdomain

You can also issue Let's Encrypt certificates with subdomains.

```bash
wo site create sub.site.tld --wp --letsencrypt
```

**Since the release v3.9.8.4**, WordOps will automatically detect if the site is a domain or a subdomain, and will not issue a certificate for www alias with subdomains

##### Wildcard

**Since the release v3.9.6**, WordOps supports Let's Encrypt Wildcard SSL certificates with DNS API validation. Before issuing a wildcard certificate, it require to define the DNS API crendentials for acme.sh.

<asciinema-player src="/images/wositecreatewildcard.cast" autoplay loop cols="120" rows="30"></asciinema-player>

Example with Cloudflare DNS:

```bash
export CF_Key="d7eab56a903f25dd4xxxxxxxxxxxxxxxxxxxx"
export CF_Email="email@domain.com"
```

!!! info

<!-- prettier-ignore -->
    More example in our guide about [DNS API configuration](/how-to/configure-letsencrypt-dns-api-validation)

<!-- prettier-ignore-end -->

After you define those variables with the command `export`, you can issue your certificate with

```bash
wo site create site.tld --wp --letsencrypt=wildcard --dns=dns_cf
```

-   `--dns=dns_cf` can be replaced with another DNS provider supported by acme.sh. For DigitalOcean, it would be `--dns=dns_dgon`

#### HSTS

Additionally you can enable HSTS on your site by adding the flag `--hsts` with `--letsencrypt`

```bash
wo site create site.tld --wp --letsencrypt --hsts
```

#### PHP 8.2 & PHP 8.2

To create site with PHP 8.2 you can use --php82 during site creation

For example, you can create WordPress site running on PHP 8.2 using following command:

```bash
wo site create site.tld --wp --php82
```

For a WordPress site running on PHP 8.3:

```bash
wo site create site.tld --wp --php83
```

To create simple php site running with PHP 8.3 with no database, you can use this command:

```bash
wo site create site.tld --php83
```

This is the same with PHP 8.2:

```bash
wo site create site.tld --php82
```

## site update

Update site configuration

### Pre-update policy

`wo site update` command follows following procedure while updating current site.

Before Updating any site:

-   Creates nginx configuration backup for site.
-   Moves htdocs to backup while updating HTML/PHP/MySQL site.
-   Creates database dump in backup.
-   While updating current MySQL site WordOps uses same database for installing WordPress tables.
-   All these backup are stored outside htdocs, in backup directory.

### WordOps possible Update Options

<style type="text/css">.ritz .waffle a{color:inherit}.ritz .waffle .s2{border-bottom:1px SOLID #000;border-right:1px SOLID #000;background-color:#666;text-align:center;color:#fff;font-family:'Arial';font-size:10pt;vertical-align:bottom;white-space:nowrap;direction:ltr;padding:2px 3px 2px 3px}.ritz .waffle .s10{border-bottom:1px SOLID #000;border-right:1px SOLID #000;background-color:#f3f3f3;text-align:center;color:#6aa84f;font-family:'Arial';font-size:10pt;vertical-align:bottom;white-space:nowrap;direction:ltr;padding:2px 3px 2px 3px}.ritz .waffle .s11{border-bottom:1px SOLID #000;border-right:1px SOLID #000;background-color:#fff;text-align:center;color:#cc4125;font-family:'Arial';font-size:10pt;vertical-align:bottom;white-space:nowrap;direction:ltr;padding:2px 3px 2px 3px}.ritz .waffle .s9{border-bottom:1px SOLID #000;border-right:1px SOLID #000;background-color:#f3f3f3;text-align:center;color:#cc4125;font-family:'Arial';font-size:10pt;vertical-align:bottom;white-space:nowrap;direction:ltr;padding:2px 3px 2px 3px}.ritz .waffle .s3{border-right:none;border-bottom:1px SOLID #000;background-color:#666;text-align:center;color:#fff;font-family:'Arial';font-size:10pt;vertical-align:bottom;white-space:nowrap;direction:ltr;padding:2px 3px 2px 3px}.ritz .waffle .s1{border-bottom:1px SOLID #000;border-right:1px SOLID #000;background-color:#fff;text-align:left;color:#000;font-family:'Arial';font-size:10pt;vertical-align:bottom;white-space:nowrap;direction:ltr;padding:2px 3px 2px 3px}.ritz .waffle .s4{border-left:none;border-right:none;border-bottom:1px SOLID #000;background-color:#666;text-align:center;color:#fff;font-family:'Arial';font-size:10pt;vertical-align:bottom;white-space:nowrap;direction:ltr;padding:2px 3px 2px 3px}.ritz .waffle .s6{border-bottom:1px SOLID #000;border-right:1px SOLID #000;background-color:#fff;text-align:center;color:#000;font-family:'Arial';font-size:10pt;vertical-align:bottom;white-space:nowrap;direction:ltr;padding:2px 3px 2px 3px}.ritz .waffle .s5{border-left:none;border-bottom:1px SOLID #000;background-color:#666;text-align:center;color:#fff;font-family:'Arial';font-size:10pt;vertical-align:bottom;white-space:nowrap;direction:ltr;padding:2px 3px 2px 3px}.ritz .waffle .s8{border-bottom:1px SOLID #000;border-right:1px SOLID #000;background-color:#f3f3f3;text-align:center;color:#000;font-family:'Arial';font-size:10pt;vertical-align:bottom;white-space:nowrap;direction:ltr;padding:2px 3px 2px 3px}.ritz .waffle .s0{border-bottom:1px SOLID #000;background-color:#fff;text-align:center;font-weight:bold;color:#20124d;font-family:'Arial';font-size:12pt;vertical-align:bottom;white-space:nowrap;direction:ltr;padding:2px 3px 2px 3px}.ritz .waffle .s7{border-bottom:1px SOLID #000;border-right:1px SOLID #000;background-color:#fff;text-align:center;color:#6aa84f;font-family:'Arial';font-size:10pt;vertical-align:bottom;white-space:nowrap;direction:ltr;padding:2px 3px 2px 3px}</style>
<div class="ritz grid-container" dir="ltr" style="overflow: auto;"><table class="waffle" cellspacing="0" cellpadding="0"><thead><tr><th class="row-header freezebar-origin-ltr header-shim row-header-shim"></th><th id="0C0" style="width:131px" class="header-shim"></th><th id="0C1" style="width:32px" class="header-shim"></th><th id="0C2" style="width:29px" class="header-shim"></th><th id="0C3" style="width:41px" class="header-shim"></th><th id="0C4" style="width:24px" class="header-shim"></th><th id="0C5" style="width:34px" class="header-shim"></th><th id="0C6" style="width:37px" class="header-shim"></th><th id="0C7" style="width:52px" class="header-shim"></th><th id="0C8" style="width:70px" class="header-shim"></th><th id="0C9" style="width:119px" class="header-shim"></th><th id="0C10" style="width:114px" class="header-shim"></th><th id="0C11" style="width:59px" class="header-shim"></th><th id="0C12" style="width:101px" class="header-shim"></th><th id="0C13" style="width:103px" class="header-shim"></th><th id="0C14" style="width:103px" class="header-shim"></th></tr></thead><tbody><tr style="height:20px;"><th id="0R0" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s0" dir="ltr" colspan="14">WordOps Possible  Site Update Options</td><td class="s0"></td></tr><tr style="height:20px;"><th id="0R1" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s1"></td><td class="s2">html</td><td class="s2">php</td><td class="s2">mysql</td><td class="s2">wp</td><td class="s2">wpfc</td><td class="s2">wpsc</td><td class="s2">wpredis</td><td class="s3">wpsubdom</td><td class="s4 softmerge"><div class="softmerge-inner" style="width: 118px; left: -3px;">wpsubdom  +  wpfc</div></td><td class="s5 softmerge"><div class="softmerge-inner" style="width: 113px; left: -3px;">wpsubdom + wpsc</div></td><td class="s3 softmerge">wpsubdir</td><td class="s4 softmerge"><div class="softmerge-inner" style="width: 100px; left: -3px;">wpsubdir + wpfc</div></td><td class="s4 softmerge"><div class="softmerge-inner" style="width: 102px; left: -3px;">wpsubdir + wpsc</div></td><td class="s4 softmerge"><div class="softmerge-inner" style="width: 203px; left: -3px;">wpsubdir + wpsc</div></td></tr><tr style="height:20px;"><th id="0R2" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s6">html</td><td class="s6">-</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td></tr><tr style="height:20px;"><th id="0R3" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s8">php</td><td class="s9">✘</td><td class="s8">-</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td></tr><tr style="height:20px;"><th id="0R4" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s6">mysql</td><td class="s11">✘</td><td class="s11">✘</td><td class="s6">-</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td></tr><tr style="height:20px;"><th id="0R5" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s8"></td><td class="s9"></td><td class="s9"></td><td class="s9"></td><td class="s8"></td><td class="s10"></td><td class="s10"></td><td class="s10"></td><td class="s10"></td><td class="s10"></td><td class="s10"></td><td class="s10"></td><td class="s10"></td><td class="s10"></td><td class="s10"></td></tr><tr style="height:20px;"><th id="0R6" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s6">wp</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s6">-</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td></tr><tr style="height:20px;"><th id="0R7" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s8">wpfc</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s10">✔</td><td class="s8">-</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td></tr><tr style="height:20px;"><th id="0R8" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s6">wpsc</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s7">✔</td><td class="s7">✔</td><td class="s6">-</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td></tr><tr style="height:20px;"><th id="0R9" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s8">wpredis</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s8">-</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td></tr><tr style="height:20px;"><th id="0R10" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s6"></td><td class="s11"></td><td class="s11"></td><td class="s11"></td><td class="s11"></td><td class="s11"></td><td class="s11"></td><td class="s6"></td><td class="s6"></td><td class="s7"></td><td class="s7"></td><td class="s11"></td><td class="s11"></td><td class="s11"></td><td class="s6"></td></tr><tr style="height:20px;"><th id="0R11" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s8">wpsubdom</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s8">-</td><td class="s10">✔</td><td class="s10">✔</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td></tr><tr style="height:20px;"><th id="0R12" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s6">wpsubdom+wpfc</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s7">✔</td><td class="s11">-</td><td class="s7">✔</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td></tr><tr style="height:20px;"><th id="0R13" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s8">wpsubdom+wpsc</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td></tr><tr style="height:20px;"><th id="0R14" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s6">wpsubdom+wpredis</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s7">✔</td><td class="s7">✔</td><td class="s6">        -</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td></tr><tr style="height:20px;"><th id="0R15" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s8"></td><td class="s9"></td><td class="s9"></td><td class="s9"></td><td class="s9"></td><td class="s9"></td><td class="s9"></td><td class="s9"></td><td class="s9"></td><td class="s8"></td><td class="s9"></td><td class="s9"></td><td class="s10"></td><td class="s10"></td><td class="s10"></td></tr><tr style="height:20px;"><th id="0R16" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s6">wpsubdir</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">-</td><td class="s7">✔</td><td class="s7">✔</td><td class="s7">✔</td></tr><tr style="height:20px;"><th id="0R17" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s8">wpsubdir+wpfc</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s10">✔</td><td class="s8">-</td><td class="s10">✔</td><td class="s10">✔</td></tr><tr style="height:20px;"><th id="0R18" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s6">wpsubdir+wpsc</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s11">✘</td><td class="s7">✔</td><td class="s7">✔</td><td class="s6">-</td><td class="s7">✔</td></tr><tr style="height:20px;"><th id="0R19" style="height: 20px;" class="row-headers-background row-header-shim"><div class="row-header-wrapper" style="line-height: 20px;"></div></th><td class="s8">wpsubdir+wpredis</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s9">✘</td><td class="s10">✔</td><td class="s10">✔</td><td class="s10">✔</td><td class="s8">-</td></tr></tbody></table></div>
<script type='text/javascript' nonce='Xz18Z26bXmR7taAlfzModg'>
    function posObj(sheet,id,row,col,x,y) {
        var rtl=false;
        var sheetElement=document.getElementById(sheet);
        if(!sheetElement) {
            sheetElement=document.getElementById(sheet+'-grid-container');
        }
        if(sheetElement) {
            rtl=sheetElement.getAttribute('dir')=='rtl';
        }
        var r=document.getElementById(sheet+'R'+row);
        var c=document.getElementById(sheet+'C'+col);
        if(r&&c) {
            var objElement=document.getElementById(id);
            var s=objElement.style;
            var t=y;
            while(r&&r!=sheetElement) {
                t+=r.offsetTop;
                r=r.offsetParent;
            }
            var offsetX=x;
            while(c&&c!=sheetElement) {
                offsetX+=c.offsetLeft;
                c=c.offsetParent;
            }
            if(rtl) {
                offsetX-=objElement.offsetWidth;
            }
            s.left=offsetX+'px';
            s.top=t+'px';
            s.display='block';
            s.border='1px solid #000000';
        }
    };
    function posObjs() {
    };
    posObjs();</script>

Example: updating site from basic wp to wp + fastcgi_cache:

<asciinema-player src="/images/wositeupdate.cast" autoplay loop cols="120" rows="30"></asciinema-player>

### Usage

Usage:

```bash
wo site update  [<site_name>] [options]
```

| options                             | description                                                            |
| ----------------------------------- | ---------------------------------------------------------------------- |
| `--html`                            | update to html site                                                    |
| `--php`                             | update to php site                                                     |
| `--mysql`                           | update to MySQL + PHP site                                             |
| `--php74`                           | update site to PHP 7.4                                                 |
| `--php80`                           | update site to PHP 8.0                                                 |
| `--php81`                           | update site to PHP 8.1                                                 |
| `--php82`                           | update site to PHP 8.2                                                 |
| `--php82`                           | update site to PHP 8.3                                                 |
| `--wp`                              | update site to WordPress without cache                                 |
| `--wpfc`                            | update site to WordPress with fastcgi_cache                            |
| `--wpsc`                            | update site to WordPress with wp-super-cache plugin                    |
| `--wpredis`                         | update site to WordPress with redis-cache                              |
| `--wprocket`                        | update site to WordPress with WP-Rocket plugin                         |
| `--wpce`                            | update site to WordPress with Cache-Enabler plugin                     |
| `--wpsubdir`                        | update site to WordPress multisite on subdirectories                   |
| `--wpsubdomain`                     | update site to WordPress multisite on subdomains                       |
| `--password`                        | update admin password for a WordPress site                             |
| `--letsencrypt`,`-le`               | secure site with Let's Encrypt SSL certificate                         |
| `--letsencrypt=wildcard`            | secure site/multisite with a wildcard SSL certificates                 |
| `--letsencrypt=off`                 | disable Let's Encrypt SSL certificate                                  |
| `--dns`, `--dns=<dns api provider>` | issue Let's Encrypt certificate with DNS validation. default: `dns_cf` |
| `--hsts`, `--hsts=off`              | Enable or disable HSTS on site secured with Let's Encrypt              |
| `--ngxblocker`, `--ngxblocker=off`  | Enable or disable Ultimate Nginx bad blocker                           |

### Examples

Update a WordPress site without cache (`--wp`), to WordPress with Nginx fastcgi_cache

```bash
wo site update site.tld --wpfc
```

Update a WordPress site running with PHP 8.2 to PHP 8.3

```bash
wo site update site.tld --php83
```

Update a site running with PHP 8.3 to PHP 8.1

```bash
wo site update site.tld --php81
```

Update a site running with PHP 8.1 or PHP 8.2 to PHP 8.3

```bash
wo site update site.tld --php83
```

Update a WordPress site with Nginx fastcgi_cache to WordPress with redis-cache

```bash
wo site update site.tld --wpredis
```

## site info

Get site information including cache backend, PHP version or user database credentials

<asciinema-player src="/images/wositeinfo.cast" autoplay loop cols="120" rows="30"></asciinema-player>

Usage:

```bash
wo site info [<site_name>]
```

## site delete

Delete site including webroot and database:

Usage:

```bash
wo site delete  [<site_name>] [options]
```

| options       | description                                |
| ------------- | ------------------------------------------ |
| `--no-prompt` | delete website without confirmation prompt |
| `--files`     | delete only website files                  |
| `--db`        | delete only database                       |

## site edit

Edit site Nginx configuration

<asciinema-player src="/images/wositeedit.cast" autoplay loop cols="125" rows="30"></asciinema-player>

Usage:

```bash
wo site edit [<site_name>]
```

You will be prompted to choose the text editor you prefer. Nano is highly recommended for beginners.

## site cd

Move into a site webroot directory

<asciinema-player src="/images/wositecd.cast" autoplay loop cols="125" rows="30"></asciinema-player>

Usage:

```bash
wo site cd  [<site_name>]
```

## site list

List all sites managed with WordOps

<asciinema-player src="/images/wositelist.cast" autoplay loop cols="125" rows="30"></asciinema-player>

Usage:

```bash
wo site list
```

## site show

Display site Nginx configuration

<asciinema-player src="/images/wositeshow.cast" autoplay loop cols="125" rows="30"></asciinema-player>

Usage:

```bash
wo site show  [<site_name>]
```

## site disable

Disable site Nginx vhost

Usage:

```bash
wo site disable  [<site_name>]
```

## site enable

Enable site Nginx vhost

Usage:

```bash
wo site enable  [<site_name>]
```
