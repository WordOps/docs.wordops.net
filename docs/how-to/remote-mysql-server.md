# Use WordOps with a remote MySQL server

By default, if there is no local MySQl server available, WordOps will install MySQL stack for any site that require a MySQL database.
But you can easily configure WordOps to use a remote MySQL server. Here the steps to follow.

## Install MySQL client

This can be done with the command :

```bash
wo stack install --mysqlclient
```

## Allow remote root connection on the remote server

Login into your remote MySQL server and grant privileges to root from a remote address :

```bash
# allow root from any address with %
mysql -e "grant all privileges on *.* to 'root'@'%'  IDENTIFIED BY 'your-very-strong-password' with grant option;"

# allow root access from a specific address (192.168.1.60)
mysql -e "grant all privileges on *.* to 'root'@'192.168.1.60'  IDENTIFIED BY 'your-very-strong-password' with grant option;"
```

Then apply changes with :

```bash
# flush privileges to appply changes
mysql -e "flush privileges;"
```

Also make sure the line `bind 127.0.0.1` is commented in /etc/mysql/my.cnf. Otherwise, comment it and restart mysql.

## Set remote MySQL server credentials

On your WordOps server, create the file `/etc/mysql/conf.d/my.cnf` and set your remote MySQL server crendentials, it should look like this example :

```bash
[client]
host = 192.168.1.10
user = root
password = your-very-strong-password
```

## Update Wordops configuration

This is the last step to use your remote MySQL server, update the variable `grant-host` in `/etc/wo/wo.conf` by replacing `localhost` by `%` or your server IP.

```bash
[mysql]

### MySQL database grant host name
grant-host = %
```