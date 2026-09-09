# Day 37 – Azure PHP Application with Remote MySQL

## Objective

Connect a PHP application running on an Azure VM to a MySQL database running on another Azure VM.

## Resources Created

### MySQL VM

* VM Name: `datacenter-mysql-vm`
* Region: `Central US`
* Image: Jetware Percona Server for MySQL
* Image URN: `jetware-srl:percona_mysql:percona_mysql57-ubuntu-1604:1.0.170503`
* Size: `Standard_B1s`
* Authentication: Password
* OS Disk: Standard HDD (`Standard_LRS`)
* Public IP: `23.99.141.10`
* SSH Port: `22`
* MySQL Port: `3306`

### Network Security

Added an inbound NSG rule allowing MySQL traffic:

* Rule: `open-port-3306`
* Port: `3306`
* Protocol: TCP
* Direction: Inbound
* Access: Allow

SSH on port 22 was also enabled.

## MySQL Configuration

Entered the Jetware MySQL environment:

```bash
sudo /jet/enter mysql
```

Created the database:

```sql
CREATE DATABASE datacenter_db;
```

Created the remote-access MySQL user:

```sql
CREATE USER 'datacenter_user'@'%' IDENTIFIED BY 'password123';
```

Granted database privileges:

```sql
GRANT ALL PRIVILEGES ON datacenter_db.* TO 'datacenter_user'@'%';
```

Applied privileges:

```sql
FLUSH PRIVILEGES;
```

### Verification

Database was verified with:

```sql
SHOW DATABASES;
```

`datacenter_db` was present.

User was verified with:

```sql
SELECT User, Host
FROM mysql.user
WHERE User = 'datacenter_user';
```

Result:

```text
datacenter_user | %
```

Privileges were verified with:

```sql
SHOW GRANTS FOR 'datacenter_user'@'%';
```

The user had:

```text
GRANT ALL PRIVILEGES ON `datacenter_db`.* TO 'datacenter_user'@'%'
```

MySQL was verified listening on port 3306:

```bash
sudo ss -lntp | grep 3306
```

Result:

```text
LISTEN ... :::3306 ... mysqld
```

## PHP VM

Existing VM:

* VM Name: `datacenter-php-vm`
* Public IP: `20.169.170.137`

Existing PHP application:

```text
/var/www/html/db_test.php
```

Created a backup:

```bash
sudo cp /var/www/html/db_test.php /var/www/html/db_test.php.bak
```

Updated the PHP database connection to:

```php
$servername = "23.99.141.10";
$username = "datacenter_user";
$password = "password123";
$dbname = "datacenter_db";
$port = 3306;

$conn = new mysqli($servername, $username, $password, $dbname, $port);
```

## PHP Validation

Syntax check:

```bash
php -l /var/www/html/db_test.php
```

Result:

```text
No syntax errors detected in /var/www/html/db_test.php
```

Local application test:

```bash
curl -s http://localhost/db_test.php
```

Result:

```text
Connected successfully
```

## Final End-to-End Validation

From the Azure lab client:

```bash
curl -s http://20.169.170.137/db_test.php
```

Result:

```text
Connected successfully
```

## Final Status

Day 37 is successfully completed.

The PHP application on `datacenter-php-vm` can remotely connect to the MySQL database on `datacenter-mysql-vm` through Azure networking and TCP port 3306.