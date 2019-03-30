# Installation Guide

Welcome in WordOps installation guide. WordOps can be installed on Debian 8 (Jessie) or Debian 9 (stretch) as well as on Ubuntu 16.04 LTS(xenial) or  Ubuntu 18.04 LTS(bionic).

## Automated Installation

We provide an installer script which install the required dependencies, before setting-up WordOps. It can be installed with the following command :

```bash
wget -qO wo wordops.se/tup && sudo bash wo
```

## Manual Installation

If you prefer to perform yourself the same steps than our installer script, here how to install WordOps manually.

### Install WordOps dependencies

```bash
# On Ubuntu
apt-get install build-essential curl gzip python3 python3-apt python3-setuptools python3-dev sqlite3 git tar software-properties-common pigz gnupg2 fail2ban cron ccze rsync -y

# On Debian
apt-get install build-essential curl gzip dirmngr sudo python3 python3-apt python3-setuptools python3-dev ca-certificates sqlite3 git tar software-properties-common pigz apt-transport-https gnupg2 fail2ban cron ccze rsync -y
```

### Clone the github repository

```bash
git clone https://github.com/WordOps/WordOps.git
```

### Install WordOps

```bash
cd WordOps/
python3 setup.py install
```
