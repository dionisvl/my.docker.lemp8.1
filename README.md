<p><img alt="laravel" src="https://laravel.com/assets/img/components/logo-laravel.svg"></p>

## Docker LEMP stack with PHP 8.1

- and Laravel Pusher example

## How to Install

- Install Docker and Compose plugin https://docs.docker.com/engine/install/
- `mkdir /var/www/my.site` and `cd /var/www/my.site`
- add `127.0.0.1 site.local` to your hosts file
- `git clone THIS_REPO ./`
- `cp .env.example .env`
- `cp app/.env.example app/.env`
- fill all `MAIL_*` params in `app/.env` file
- make sure that ALL params filled correctly in both files: `.env` and `app/.env`
- `make composer-install`
- `php artisan storage:link --relative`
- `sudo chown -R www-data:www-data /var/www/my.site/app/storage`
- `sudo chown -R www-data:www-data /var/www/my.site/app/bootstrap`
- `sudo chmod 644 /var/www/my.site/.docker/db/my.cnf`
- `make migrate-seed`
- Optional:
  see how to create demo items in `Factories.md` file.

### Deployment

- `make down`
- `git pull`
- `docker compose up --build -d`
- optional: `make composer-install`
- optional: `make migrate`

### Cache

```
php artisan optimize:clear
composer dump-autoload
composer cc
```
