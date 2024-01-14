# Simple Laravel Queue Job

## Installation

```bash
$ git clone https://github.com/fdjrr/queue.git
$ cd queue
$ composer update
$ cp .env .env.example
$ php artisan key:generate
$ php artisan migrate
```

## Configuration

```bash
FILESYSTEM_DISK=public
QUEUE_CONNECTION=database
```

## Installing Supervisor

```bash
$ sudo apt-get install supervisor
```

## Configuring Supervisor

```bash
$ sudo nano /etc/supervisor/conf.d/laravel-worker.conf
```

```bash
[program:laravel-worker]
process_name=%(program_name)s_%(process_num)02d
command=php /home/forge/app.com/artisan queue:work --sleep=3 --tries=3 --max-time=3600
autostart=true
autorestart=true
stopasgroup=true
killasgroup=true
user=forge
numprocs=8
redirect_stderr=true
stdout_logfile=/home/forge/app.com/worker.log
stopwaitsecs=3600
```

## Starting Supervisor

```bash
$ sudo supervisorctl reread

$ sudo supervisorctl update

$ sudo supervisorctl start "laravel-worker:*"
```

## Restarting and Reloading

```bash
$ sudo supervisorctl restart "laravel-worker:*"
```
