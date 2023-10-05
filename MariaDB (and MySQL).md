Start it:

```shell
sudo systemctl start mariadb
```

There's a wizard to change root password and perform other security-related tasks. Run it:

```shell
sudo mysql_secure_installation
```

To delete a database in phpMyAdmin, select the database and go to the operations tab.

Show all databases (within the monitor console):
```MariaDB
show databases;
```

Remember to run 
```MariaDB
flush privileges;
```
after creating/altering users!

Daemon options
```shell
--log-ddl-recovery=$(pwd)/<log file name> #assumed to be relative to be the MariaDB data dir. Use an absolute dir to put it elsewhere.

--aria-log-dir-path=/home/patrick/Code/my_final_homepage/.devbox/virtenv/mariadb/run/aria

--innodb-data-file-path=/home/patrick/Code/my_final_homepage/.devbox/virtenv/mariadb/data/ibdata1:12M #note that size specified after the colon
```

