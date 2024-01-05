# Backend Configuration

##

## Firebase Setup & Configuration

Go to [https://firebase.google.com/](https://firebase.google.com/) create your project using the app name\
click the project setting from project overview dropdown

<figure><img src="../.gitbook/assets/Screenshot 2023-10-30 at 4.33.23 PM.png" alt=""><figcaption></figcaption></figure>

copy the project ID and web API key to your admin ->settings -> firebase api key

<figure><img src="../.gitbook/assets/Screenshot 2023-10-30 at 4.30.10 PM.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2023-10-30 at 4.17.45 PM.png" alt=""><figcaption></figcaption></figure>



The cron job is very important

open your crontab and paste the code below, make sure you use your project absolute path

```
* * * * * cd /var/www/html/ride_surd && php artisan schedule:run >> /dev/null 2>&1
```

##

## Queue Setup(optional)

for sending notifications we need to configure the supervisor setup to run the queue jobs, this is not compulsory but necessary for effective queue processing, follow the  setup here&#x20;

{% embed url="https://laravel.com/docs/10.x/queues#supervisor-configuration" %}

sample laravel-worker file

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

## Setup Cron Job

## Introduction

You are almost done and ready to complete your setup,

login [http://your-base-url/login](http://your-base-url/login)

enter your login details



## Complete your admin setup

<figure><img src="../.gitbook/assets/Screenshot 2023-10-30 at 4.23.45 PM.png" alt=""><figcaption></figcaption></figure>

Complete the general settings, smtp, mobile app setting, firebase and map API settings, payment methods and trip settings

<figure><img src="../.gitbook/assets/Screenshot 2023-10-30 at 4.18.42 PM.png" alt=""><figcaption></figcaption></figure>

