# MySQL Cheat Sheet

MySQL commands and useful stuff for working with this RDBMS.

## Commands

### Create User

```
CREATE USER 'user_name'@'localhost' IDENTIFIED BY 'password';
```

### Grant User Privileges

Grant permissions to work on database(s):

```
GRANT ALL PRIVILEGES ON *.* TO 'user_name'@'localhost';
```

Reload privileges so the RDBMS knows about the user:

```
FLUSH PRIVILEGES;
```

### List users in MySQL Server

Login as an administrative user to the `mysql` client:

```bash
$ mysql -u root -p
```

Then, you can list users with:

```
mysql> select * from mysql.user;
```

Notice this list all fields from the table. You can filter to get a better overview of the table:

```
mysql> select host, user, password from mysql.user;
```

You can always see what fields to list with:

```
mysql> desc mysql.user;
```

### Backup & Recover Database

Backup database:

```
mysql -u [USER_NAME] -p [DB_NAME] > dump.sql
```

Recover database from dump:

```
mysql -u [USER_NAME] -p [DB_NAME] < dump.sql
```

## Vagrant

Once you install MySQL server in a vagrant machine you can access that DB by SSHing into the vagrant box and then login in to the mysql CLI. However, if you'd like to have a visual representation or use a GUI, such a WorkBench, for easy manage of the database, some additional setup is needed.

### Change `bind-address` to Access Database from Vagrant Host

First, you need to change the bind-address in the mysql configuration file (located in /etc/mysql/my.conf).

Open your mysql conf file:

```
sudo nano /etc/mysql/my.conf
```

Find the line with `bind-address` and change to something like:

```
bind-address = 0.0.0.0
```

Restart MySQL server to load new setting:

```
sudo service mysql restart
```

### Access MySQL Server from WorkBench in Vagrant Host

```
Connection Method: Standard TCP/IP over SSH
SSH Hostname: [127.0.0.1:2222] or virtual machine IP and port
SSH Username: vagrant
SSH Password: vagrant
MySQL Hostname: 127.0.0.1
MySQL Server Port: 3306
Username: root
Password: [root-password]
```

Sometimes you'd need to specify an ssh key file. See full configuration below:

<img src="https://trello-attachments.s3.amazonaws.com/57ead188bcc0accfbdeb5e8b/57ead1b10ee527861de2f2dc/5779ec406533e76e8167db7520d44dd0/workbench-bd-access.png" alt="configure-workbench-for-vagrant" />

## WordPress

WordPress, for whatever design reason, saves url in two places: database and `wp-config.php` file. When not saved in config file, not having a correct value in the database causes mayhem in the WordPress installation.

With this query you can find set values for `siteurl` and `home` values in the `wp_options` table of a WordPress installation:

```
SELECT * FROM [db_name].wp_options
WHERE option_name = 'siteurl'
OR option_name = 'home';
```

## References

1. [Create a New User in MySQL](https://www.digitalocean.com/community/tutorials/how-to-create-a-new-user-and-grant-permissions-in-mysql)
2. [Change MySQL server bind-address to access db outside Vagrant](https://stackoverflow.com/questions/10709334/how-to-connect-to-mysql-server-inside-virtualbox-vagrant#10794530)
3. [List MySQL Users](https://alvinalexander.com/blog/post/mysql/show-users-i-ve-created-in-mysql-database)