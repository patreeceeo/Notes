Installing
1. sudo apt update
2. Install PHP
3. Install MariaDB
4. Install Apache
5. [Download](https://wordpress.org/latest.zip) and Unzip WordPress into DocumentRoot
6. Install phpMyAdmin: 
	1. sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl
	2. For the server selection, choose `apache2`
	3. Select `Yes` when asked whether to use `dbconfig-common`
	4. sudo phpenmod mbstring
	5. sudo systemctl restart apache2
	6. ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'password';
	7. GRANT ALL PRIVILEGES ON *.* TO 'myuser'@'localhost' WITH GRANT OPTION;
	8. flush privileges; (probably necessary)
	9. Do the rest of the stuff in here for security: https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-on-ubuntu-20-04
7. Create a wordpress database
8. Create a wordpress user in phpMyAdmin
	1. maybe change the host from % to localhost
	2. Grant all privileges
9. Edit wp-config.php
	1. Set database name, database password, database user, etc
10. go to /wp-admin/install.php

# Admin Fu

You can toggle whether the homepage displays the latest posts or a static page with Settings > Reading > Your homepage
# Code snippets

Add comments to page

```wordpress/html
<!-- wp:template-part {"slug":"comments","theme":"twentytwentythree","tagName":"section"} /-->
```

Add post content

```wordpress/html
<!-- wp:post-content {"layout":{"type":"constrained"}} /-->
```
