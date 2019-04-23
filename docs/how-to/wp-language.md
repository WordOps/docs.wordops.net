# How to set default language for WordPress install

WordOps uses WP-Cli to install and perform other tasks on WordPress blogs.

The default language for new blogs is `en_US` but it can be easily adapted to any other locale.

WP-Cli expects a configuration file to be placed on `~/.wp-cli/config.yml`. We won't cover all its possibilities right now, only the configuration required to customize the localisation.

For example, in order to have WordPress in Brazilian Portuguese the `config.yml` file would be:

```yaml
core download:
  locale: pt_BR
```

## Caveats

There is a "caveat" one should be aware of: when a new version os WordPress is released it usually does not have translations for all possible locales. Setting up a configuration file like the suggestion above might lead to WP-Cli (thus WordOps) to behave inconsistently.

## How to change locale of a blog already installed

In order to avoid such inconsistence, perhaps it's wiser to install WP in `en_US` as usual, then later change its locale. The root user would do:

```bash
cd /var/www/example.com/htdocs
wp language core install pt_BR --activate --allow-root
```
