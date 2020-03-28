# Install and fix password issue for mysql

## Install required package

```bash
sudo apt install build-essential libreadline-dev libxml2-dev libxslt1-dev libcurl4-openssl-dev libmysqlclient-dev
```

## Install mysql

```bash
sudo apt install mysql-server -y
```

## Stop mysql service and start mysql in safe mode without a password

```bash
sudo service mysql stop
sudo mkdir -p /var/run/mysqld
sudo chown mysql:mysql /var/run/mysqld
sudo /usr/sbin/mysqld --skip-grant-tables --skip-networking &
mysql -u root
```

## Reset password for user root

```mysql
USE mysql;
UPDATE user SET authentication_string=PASSWORD("12345678") WHERE User='root';
-- "12345678" is your password for user root
UPDATE user SET plugin="mysql_native_password" WHERE User='root';
quit
```

## Kill mysqld service and restart mysql

```bash
sudo pkill mysqld
sudo service mysql start
```

