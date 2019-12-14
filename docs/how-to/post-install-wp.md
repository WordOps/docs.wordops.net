# WordPress post-install automation

There are multiple, viable approaches to automate post-installation of a WordPress blog using WordOps, without the need of adding new commands or increasing overall complexity.

For this tutorial, we're going to show how to automatically install plugins and themes from official WordPress repository, as well as how to install custom plugins and themes, not available at wordpress.org.

## First thing first: configuring the "custom" repository

The custom plugins and themes you're going to install on your newly installed blogs must be publicly available on a particular location of your knowledge. It's from there that our script will fetch them to add to WordPress.

For example, one could store their custom plugins and themes in a GitHub repository. Or they could be available through public links in Google Drive, Dropbox, or even in a website set up just for serving this purpose — this is the approach this tutorial will cover.

We'll save our plugins and themes in zip format, just following the standard. For this example, assume the subdomain `downloads.sarmento.org` is our repository, and the files are saved at the root level.

Examples:

- `https://downloads.sarmento.org/customplugin.zip`
- `https://downloads.sarmento.org/awesometheme.zip`

## The script itself

Save your script at an easy to remember location, e.g. `/scripts/post-wp-install.sh` and give it execution permission:

```bash
chmod +x /scripts/post-wp-install.sh
```

The contents of the script should be something like this, adapted to your own needs, of course:

```bash
#! /bin/bash

DOM=$1
if test -z $DOM ; then
    echo "ERROR: no domain informed!"
    exit 1
fi

if [ ! -e "/var/www/${DOM}/wp-config.php" ] ; then
    echo "ERROR: ${DOM} does not appear to be a valid WordPress!"
    exit 1
fi

cd "/var/www/${DOM}/htdocs"

### Install plugins from official repository
wp plugin install wordpress-seo --allow-root --activate
wp plugin install wordpress-hide-login --allow-root --activate

### Install custom plugin
wp plugin install https://downloads.sarmento.org/customplugin.zip --allow-root
wp plugin activate customplugin --allow-root

### Install custom theme
wp theme install https://downloads.sarmento.org/awesometheme.zip --allow-root
wp theme activate awesometheme --allow-root

### Fix permissions
chown www-data:www-data wp-content -R
cd -

exit 0
```

### Example of how to use the script

```bash
# install the blog
wo site create thedomain.com --wpredis --php73
/scriprs/post-wp-install.sh thedomain.com
```

### Notes about the script

Except for the two "ifs" that check whether the domain was informed as a parameter and whether it is a valid WordPress, there is no complicated logic, just a sequence of commands.

It is the most simple and effective way of standardizing the post installation of blogs using the tools already included in WordOps.
