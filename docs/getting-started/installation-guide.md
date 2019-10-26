# Installation

## One-Step Automated Install

![wordops-install](https://netdata.wordops.eu/netdata/api/v1/badge.svg?chart=web_log_wops.cc.requests_per_url&options=unaligned&dimensions=download&group=sum&after=-86400&label=today&units=installations&precision=0)

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
# On Ubuntu
apt-get install build-essential bash-completion curl gzip python3 \
python3-apt python3-setuptools python3-dev sqlite3 git tar \
software-properties-common pigz gnupg2 cron ccze rsync -y

# On Debian
apt-get install build-essential bash-completion curl gzip dirmngr \
sudo python3 python3-apt python3-setuptools python3-dev  \
ca-certificates sqlite3 git tar software-properties-common \
pigz apt-transport-https gnupg2 cron ccze rsync -y
```

### Clone the github repository

```bash
git clone https://github.com/WordOps/WordOps.git
```

create log directory

```bash
mkdir -p /var/log/wo
```

### Install WordOps

```bash
cd WordOps/
python3 setup.py install
```

### Install acme.sh

```bash
# clone the repository
git clone <https://github.com/Neilpang/acme.sh.git> /opt/acme.sh -q

# create conf directory
mkdir -p /etc/letsencrypt/{config,live,renewal}

# install acme.sh
cd /opt/acme.sh
./acme.sh --install \
            --home /etc/letsencrypt \
            --config-home /etc/letsencrypt/config \
            --cert-home /etc/letsencrypt/renewal

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
