---
hide:
  - navigation
  - toc
---

A migration is needed to migration from 1.4 to 2.1.

### Preparations and considerations.

1. First migrate to at least the 1.4.10 release if you have not already done so.
2. The signer does not require any migration. Backward (only) compatibility is respected from earlier 1.4 release.
3. If you have tooling around OpenDNSSEC you should be aware that some command line utilities and log reporting have changed. A fair amount of backward compatibility has been respected, but changes are present, some of these changes are mentioned below.
4. Due to structural changes in the Enforcer database, an automated migration of the enforcer state is required. Access to the HSM is needed during the migration but no changes in the HSM are made. You should backup your configuration and kasp.db (advised /var/opendnssec and /etc/opendnssec).
5. Many distributions do not include the migration scripts in their package. If you are missing the mysql_convert.sql and/or sqlite_convert.sql scripts in your distribution, access them from the source distribution. You can still use the binaries from your distribution and only use the uncompiled source to access these scripts.
6. No up-to-date scripts are provided to switch between SQLite and MySQL database back-end at this time.
7. Migration during a key roll (i.e. keys in state publish) especially KSK, will involve assumptions in the migration, so if possible perform the migration outside of a key roll period.

### Conversion steps

1. First stop OpenDNSSEC entirely.
2. Make sure you have backups in place of /var/opendnssec and /etc/opendnssec (or equivalent if installed under a different prefix).
3. Also prevent any nameserver from receiving updates from OpenDNSSEC until you are sure the migration was successful. No ill effects can occur but this is just common sense.
4. In case you have an SQLite installation execute the convert_sqlite script from the enforcer/utils/1.4-2.0_db_convert directory from the source distribution (or from your packaged distribution).
5. Call the script like so: ./convert_sqlite -i INPUT -o OUTPUT. Where INPUT is the kasp.db file commonly found in /var/opendnssec/kasp.db. And OUTPUT is a non-existing file where the new database should go. On success, replace old database file with the new database file accordingly.
6. In case you have an MySQL/MariaDB installation execute the convert_mysql script from the enforcer/utils/1.4-2.0_db_convert directory from the source distribution (or from your packaged distribution).
7. Call the script like so: ./convert_sqlite -i INPUT -o OUTPUT -h HOST -u USER -p PASSWORD. Where INPUT is the name of the existing database on HOST. And OUTPUT is a non-existing database on the same host where the new database should go. On success, replace old database with the new database file or adjust conf.xml accordingly.
8. Review your configuration file. Potentially the following items need editing:
  - The `<Interval>` element wasn’t relevant anymore and is now been dropped entirely and must be removed from the configuration. The Enforcer now wakes as needed rather than periodically.
  - The `<MySQL><Host>` child element is now mandatory. Set to localhost as content if not present. The Port attribute must also be present during migration. For example: `<Datastore><MySQL><Host Port="3306">&localhost</Host<...`
9. Now run the command ods-migrate to complete the migration. This command accesses the HSM to compute keytags and stores them in the enforcer database.
10. When coming from ODS1.4 you need to copy the file /etc/opendnssec/zonelist.xml to /var/opendnssec/enforcer/zones.xml

Your OpenDNSSEC installation is now ready to use.

### Review the migration and changes.

Much of the error reporting of OpenDNSSEC takes place through syslog. Be sure to inspect the syslog for any errors after and during migration.

1. Changed wake-up behavior from signer
2. Immediate rollover after migration might take longer
3. Timeout on MySQL database
4. Key states more fine grained
