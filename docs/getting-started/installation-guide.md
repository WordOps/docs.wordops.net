# Installation

## One-Step Automated Install

![PyPI - Downloads](https://img.shields.io/pypi/dw/wordops.svg?cacheSeconds=86400)

We provide an installer script which install the required dependencies, before setting-up WordOps. It can be installed with the following command:

```bash
wget -qO wo wops.cc && sudo bash wo
```

??? Info "What are the tasks performed by the install script ?"
    - Installing WordOps dependencies
    - Enabling automated security updates with unattended-upgrades
    - Enabling NTP World Time Synchronization
    - Detecting a previous EasyEngine or WordOps installation
    - Importing existant sites into WordOps
    - Installing WP-CLI
    - Installing Acme.sh
    - Installing Wordops

### Alternative: Clone Github repository and run

```bash
git clone https://github.com/WordOps/WordOps.git
cd WordOps/
sudo bash install
```

!!! info
    During the installation, you will be prompt for an username and an email address. WordOps need those informations to configure Git version control and to use it for saving server configurations. Your informations will **only be stored** in the file .gitconfig.

---

## Manual Installation

If you prefer to perform yourself the same steps than our installer script, here how to install WordOps manually.

### Install WordOps dependencies

```bash
# update packages list
apt-get update

# On Ubuntu
apt-get -option=Dpkg::options::=--force-confmiss --option=Dpkg::options::=--force-confold --assume-yes install \
build-essential curl gzip python3-pip python3-wheel python3-apt python3-setuptools python3-dev sqlite3 git tar software-properties-common pigz \
gnupg2 cron ccze rsync apt-transport-https tree haveged ufw unattended-upgrades tzdata ntp

# On Debian
apt-get -option=Dpkg::options::=--force-confmiss --option=Dpkg::options::=--force-confold --assume-yes install \
build-essential curl gzip dirmngr sudo python3-pip python3-wheel python3-apt python3-setuptools python3-dev ca-certificates sqlite3 git tar \
software-properties-common pigz apt-transport-https gnupg2 cron ccze rsync tree haveged ufw unattended-upgrades tzdata ntp
```

### create WordOps directories

```bash
mkdir -p /var/log/wo /var/lib/wo/tmp /var/lib/wo-backup
```

### Update PIP

```bash
python3 -m pip install -U pip
python3 -m pip install -U setuptools wheel
```

### Install WordOps

```bash
# install wordops from PyPi
python3 -m pip install -U wordops

# copy configuration
cp -rf /usr/local/lib/python3.*/dist-packages/usr/* /usr/
cp -rn /usr/local/lib/python3.*/dist-packages/etc/* /etc/
cp -f /usr/local/lib/python3.*/dist-packages/etc/bash_completion.d/wo_auto.rc /etc/bash_completion.d/wo_auto.rc
```

### Install acme.sh

```bash
# clone the repository
git clone https://github.com/Neilpang/acme.sh.git /opt/acme.sh -q

# create conf directory
mkdir -p /etc/letsencrypt/{config,live,renewal}

# install acme.sh
cd /opt/acme.sh
./acme.sh --install \
            --home /etc/letsencrypt \
            --config-home /etc/letsencrypt/config \
            --cert-home /etc/letsencrypt/renewal

# enable auto-upgrade
/etc/letsencrypt/acme.sh --config-home '/etc/letsencrypt/config' --upgrade --auto-upgrade

# create .well-known directory
mkdir -p /var/www/html/.well-known/acme-challenge

# set www-data as owner
chown -R www-data:www-data /var/www/html /var/www/html/.well-known

# set permissions
chmod 750 /var/www/html /var/www/html/.well-known
```

### Install WP-CLI

```bash
wget -qO /usr/local/bin/wp https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
chmod +x /usr/local/bin/wp
```
