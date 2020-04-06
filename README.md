# iocage-plugin-nextcloud_nossl

## Post install steps
### Configure Nextcloud
```
iocage get -P dnsname jail_name
iocage set -P dnsname="nextcloud.domain.tld" jail_name
```
```
iocage get -P timezone jail_name
iocage set -P timezone="Europe/Vienna" jail_name
```
