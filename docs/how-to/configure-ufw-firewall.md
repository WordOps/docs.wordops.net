# How to configure UFW Firewall

## Install UFW



```bash
sudo apt update && sudo apt install ufw -y
```

### Check what is your SSH Port

```bash
grep "Port" /etc/ssh/sshd_config
```

### Add default rules

```bash
##  enable logging
sudo ufw logging low

##  Use the default rules to allow outgoing traffic and to deny all incoming traffic.
sudo ufw default allow outgoing
sudo ufw default deny incoming

## allow SSH - DNS - HTTP and HTTPS  - NTP
sudo ufw limit 22 # can be replaced with a custom port
sudo ufw allow http
sudo ufw allow https
sudo ufw allow 123

## WordOps backend
sudo ufw allow 22222

## FTP stack
sudo ufw allow 21
sudo ufw allow 49000:50000/tcp
```

You can check what ports are currently used on your server with the following command :

```bash
sudo netstat -tulpn
```

## Enabling UFW

```bash
sudo ufw enable
```