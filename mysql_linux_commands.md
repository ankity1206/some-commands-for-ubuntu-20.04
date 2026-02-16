## Command to reset root password

### Step 1: Stop the Database
```bash
sudo systemctl stop mysql
```
### Step 2:
The temporary directory MySQL uses to communicate (/var/run/mysqld) is deleted whenever the service is stopped.
```bash
sudo mkdir -p /var/run/mysqld
sudo chown mysql:mysql /var/run/mysqld
```

### Step 3: Start MySQL in Safe Mode
```bash
sudo mysqld_safe --skip-grant-tables --skip-networking &
```

### Step 4:Log in and Reset Password 
Connect: 
```bash
mysql -u root
```
Reset: Inside the MySQL prompt, run
```sql
FLUSH PRIVILEGES;
ALTER USER 'root'@'localhost' IDENTIFIED BY 'NewPassword123';
FLUSH PRIVILEGES;
EXIT;
```

### Step 5:  Restart Normally
Kill the safe process and restart the regular service:
```bash
sudo pkill mysqld
sudo systemctl start mysql
```

### Step 6: Enter the MySQL Shell
```bash
mysql -u root -p
```
