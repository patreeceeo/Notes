There's a wizard to change root password and perform other security-related tasks. Run it:

```
sudo mysql_secure_installation
```

To delete a database in phpMyAdmin, select the database and go to the operations tab.

Show all databases (within the monitor console):
```
show databases;
```

Remember to run 
```
flush privileges;
```
after creating/altering users!