BOSH release for Postgres-Backup
===============================

Monit scripts adding backup jobs to cron. Backups are stored in `/var/vcap/store/postgres/pg_dumps`

Usage
-----

To each of your BOSH deployments, add the following:

```yaml
releases:
- name: postgres-backup
  version: latest
...
```

Add the boshdb_backup job template in case using release with `bosh deployment postgres` :

```yaml
jobs:
- name: postgres
  templates:
  - name: postgres
    release: postgres
  - name: boshdb_backup
    release: postgres-backup
```

Add the cfdb_backup job template in case using release with `cloud foundry deployment postgres` :

```yaml
jobs:
- name: postgres
  templates:
  - name: postgres
    release: postgres
  - name: cfdb_backup
    release: postgres-backup
```

Configuration
-------------

You can configure job using global properties in your manifest:

For Bosh postgres :

```yaml
properties:
  boshdb_backup:
    keep_duration: 5
    cron_duration: 4 
```
For CF postgres:

```yaml
properties:
  cfdb_backup:
    keep_duration: 5
    cron_duration: 4
```

keep duration in n number of recent backups which you want to keep on local disk.
Cron duration is the hour cycle for backup cronjob
# Author
[Ronak Banka](https://github.com/ronakbanka), (Rakuten, Inc)
