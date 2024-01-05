# Server Installation

### 1. Introduction

You can use any server that has terminal access for demo purpose, but to run effectively on production environment we would recommend the requirements below.

* Any server with UBUNTU Preferred
* 2 GB Ram
* 30 GB Storage
* vCPU 2 cores

### **2. Installation Requirement**&#x20;

1. Apache
2. PHP8.1
3. mysql
4. phpmyadmin
5. composer
6. Git
7. Laravel Supervisor (optional)

### 3. Server Setup (skip the below steps if using control panel)

### 3.1. Install Apache

* Open the ssh terminal using pemfile of your aws instance
* Run "sudo apt install apache2" to install an apache2
* Run "sudo apt update"
* Run "sudo nano /etc/apache2/sites-available/000-default.conf" to edit the config follow next step.

```
<Directory /var/www/html>
        Options -Indexes
        AllowOverride All
        Require all granted
        ErrorDocument 403 "You Don't have a permission to access this URL"
        ErrorDocument 404 "Requesting Page not Found. Contact admin for further details"
  </Directory>
```

* Run "sudo service apache2 restart" to restart the apache2.
* Reference Link : [https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-20-04](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-20-04)

### 3.2.Install PHP8.1

Please follow the instrctions from the reference link below. And Install the php extensions below. **bcmath,bz2,intl,gd,mbstring,mysql,zip,fpm,curl,xml**

Reference Link : [https://computingforgeeks.com/how-to-install-php-on-ubuntu-linux-system/](https://computingforgeeks.com/how-to-install-php-on-ubuntu-linux-system/)

### 3.3.Install mysql

Run the below commands one by one

* sudo apt-get update
* sudo apt-get install mysql-server
* mysql\_secure\_installation
* sudo service mysql restart

To create a new user for mysql

* sudo mysql -u root
* use mysql;
* GRANT ALL ON _._ TO 'taxi\_user'@'%' IDENTIFIED BY 'RideSurd@123' WITH GRANT OPTION;
* FLUSH PRIVILEGES;

Reference Link : [https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04)

### 3.4. Install phpmyadmin

Open the path "var/www/html". and dowonload the phpmyadmin package using below command.

"sudo wget [https://files.phpmyadmin.net/phpMyAdmin/5.0.1/phpMyAdmin-5.0.1-all-languages.zip](https://files.phpmyadmin.net/phpMyAdmin/5.0.1/phpMyAdmin-5.0.1-all-languages.zip)"

Unzip the downloaded package and rename it to "pma".

### 3.5. Install composer

Please follow the instructions from the reference link below.

Reference Link: [https://www.digitalocean.com/community/tutorials/how-to-install-and-use-composer-on-ubuntu-20-04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-composer-on-ubuntu-20-04)

### 3.6. Install git

Please follow the instructions from the reference link below.

Reference Link: [https://www.digitalocean.com/community/tutorials/how-to-install-git-on-ubuntu-22-04](https://www.digitalocean.com/community/tutorials/how-to-install-git-on-ubuntu-22-04)

#### 3.7. Install FTP (optional)

* Follow the below instructions to install ftp on ubuntu server

1. install vsftpd - **sudo apt install vsftpd**
2. take backup of config file by following command **sudo cp /etc/vsftpd.conf /etc/vsftpd.conf.bak**
3. edit vsftpd.conf by following command **sudo nano /etc/vsftpd.conf and add the below lines at bottom of the file and save the file.**



### **4.** Setup Laravel Supervisor &#x20;

Follow the below steps for setup the laravel supervisor&#x20;



1. sudo apt-get install supervisor
2. sudo nano /etc/supervisor/conf.d/laravel-worker.conf
3. Paste the below lines in that file



```
[program:laravel-worker]
process_name=%(program_name)s_%(process_num)02d
command=php /var/www/html/project-name/artisan queue:work --sleep=3 --tries=3
autostart=true
autorestart=true
user=ubuntu
numprocs=8
redirect_stderr=true
stdout_logfile=/var/www/html/project-name/worker.log
stopwaitsecs=3600
```

Note:user can be ubuntu/root & project name should be yours

4. sudo supervisorctl reread
5. sudo supervisorctl update
6. sudo supervisorctl start laravel-worker:\*

Reference Link: [https://laravel.com/docs/8.x/queues#supervisor-configuration](https://laravel.com/docs/8.x/queues#supervisor-configuration)

***

### **5.** Upload script to server &#x20;

Whether you are using a control panel or ssh access and have completed all necessary server installation, follow the step below to upload script to server

#### 5.1. Using GIT

1. Unzip the download script
2. locate the server folder folder
3. open with a text editor, or open in a terminal
4. run git init, git commit and git push
5. On the server login via ssh, locate the dir and run git pull,
6. Install packages and complete setup by running the below commands

```bash
composer install

cp .env.example .env 

nano .env 

```

Paste your DB credentials

```
DB_PORT=3306
DB_DATABASE=your_db_name
DB_USERNAME=your_user_name
DB_PASSWORD=your_passoword

```

5.2 Using control panel file upload

upload the server folder to your cpanel

create a file .env and paste the content of .env.example



## 6. Complete your setup

open the created .env file

```
APP_URL=http://ride_surd.test
```

Set your license code and username

```
APPLICATION_KEY=""

BUYER_USERNAME="Surd"
```

Run the following commands

```bash
php artisan migrate

php artisan db:seed

php artisan storage:link
```

If everything is successful, visit https://base\_url/setup to complete setup



<figure><img src="../.gitbook/assets/Screenshot 2023-10-30 at 12.34.55 PM.png" alt=""><figcaption></figcaption></figure>

Setup your super admin login and click continue
