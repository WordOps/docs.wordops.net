# WordOps structure

## WordOps directories

| Path                    | Description             |
| ----------------------- | ----------------------- |
| `/etc/wo`               | General configuration   |
| `/var/lib/wo/dbase.db`  | WordOps sites databases |
| `/var/lib/wo/tmp`       | tmp directory           |
| `/usr/lib/wo/templates` | WordOps templates       |

## acme.sh - letsencrypt integration

| Path                    | Description                     |
| ----------------------- | ------------------------------- |
| `/etc/letsencrypt`      | acme.sh directory               |

```bash
letsencrypt
├── acme.sh # acme executable
├── acme.sh.env # env configuration
├── config/ # acme.sh configuration
├── deploy/ # internal
├── dnsapi/ # internal
├── live/ # live SSL certificates
├── notify/ # internal
└── renewal/ # certificates configuration
```
