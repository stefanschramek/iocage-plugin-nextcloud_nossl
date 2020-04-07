# iocage-plugin-nextcloud_nossl

## Post install steps
### Stop the services
```
iocage exec jail_name "service mysql-server stop"
iocage exec jail_name "service redis stop"
iocage exec jail_name "service php-fpm stop"
iocage exec jail_name "service caddy stop"
```
### Move folders
```
iocage exec jail_name "mv /mnt/files /mnt/files.tmp"
iocage exec jail_name "mv /usr/local/www/nextcloud/config /usr/local/www/nextcloud/config.tmp"
iocage exec jail_name "mv /var/db/mysql /var/db/mysql.tmp"
```
### Add mount points
```
iocage exec jail_name "mkdir -p /mnt/files"
iocage fstab -a jail_name /mnt/pool-1/apps/nextcloud/files /mnt/files nullfs rw 0 0
iocage exec jail_name "chown www:www /mnt/files"

iocage exec jail_name "mkdir -p /usr/local/www/nextcloud/config"
iocage fstab -a jail_name /mnt/pool-1/apps/nextcloud/config /usr/local/www/nextcloud/config nullfs rw 0 0
iocage exec jail_name "chown www:www /usr/local/www/nextcloud/config"

iocage exec jail_name "mkdir -p /var/db/mysql"
iocage fstab -a jail_name /mnt/pool-1/apps/nextcloud/db /var/db/mysql nullfs rw 0 0
iocage exec jail_name "chown mysql:mysql /var/db/mysql"
```
### Move files
```
iocage exec jail_name "mv /mnt/files.tmp/* /mnt/files/"
iocage exec jail_name "mv /mnt/files.tmp/.htaccess /mnt/files/"
iocage exec jail_name "mv /mnt/files.tmp/.ocdata /mnt/files/"
iocage exec jail_name "rm -R /mnt/files.tmp"

iocage exec jail_name "mv /usr/local/www/nextcloud/config.tmp/* /usr/local/www/nextcloud/config/"
iocage exec jail_name "mv /usr/local/www/nextcloud/config.tmp/.htaccess /usr/local/www/nextcloud/config/"
iocage exec jail_name "rm -R /usr/local/www/nextcloud/config.tmp"

iocage exec jail_name "mv /var/db/mysql.tmp/* /var/db/mysql/"
iocage exec jail_name "rm -R /var/db/mysql.tmp"

```
### Start the services
```
iocage exec jail_name "service mysql-server start"
iocage exec jail_name "service redis start"
iocage exec jail_name "service php-fpm start"
iocage exec jail_name "service caddy start"
```

## Configure Nextcloud
```
iocage get -P dnsname jail_name
iocage set -P dnsname="nextcloud.domain.tld" jail_name
```
```
iocage get -P timezone jail_name
iocage set -P timezone="Europe/Vienna" jail_name
```
