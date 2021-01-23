# project-alna

Add the correct *permissions*:

```
chmod -Rv o+rw backend-alna/storage
chmod -Rv o+rw frontend-alna/storage
```

Just in case (*FAQ*) - 
```
sudo chmod -Rv 2777 backend-alna/storage/logs
sudo chmod -Rv 2777 frontend-alna/storage/logs
```

Run launching up docker compose `docker-compose up -d`.

Install the assets
```
cd backend-alna;
composer install;
cp .env.example -v .env
php artisan key:generate;
cd ../frontend-alna;
composer install
npm install
php artisan key:generate
npm install --save vue jquery;
```
Run `npm run prod` and with the installation, run it again (if it asks so) till it's finished.

## Virtualization

```
cd ..
docker-compose up -d
```

## Database initialize

Get to **Redis** configuration: `REDIS_HOST=172.16.238.10` `backend-alna/.env`. 

Add MySQL credentials to `backend-alna/.env`: 
```
DB_USERNAME=docker_alna
DB_PASSWORD=TxuJAz
```

Initialize database and migrate:
```
docker container exec -it project-alna_backend-alna_1 /bin/bash
cd laravel.app
cat dist/db-init.sql | mysql -nEv
php artisan migrate
exit
```

Run units on *SOLID DDD*:
```
docker container exec -it project-alna_backend-alna_1 /bin/bash
cd laravel.app
./vendor/bin/phpunit
exit
```

Don't get afraid *if it fails on some units*, or *warnings are issued* because its *DDD* and *documentation* discrepancies.

Start queue processing:
```
docker container exec -it project-alna_backend-alna_1 /bin/bash
cd laravel.app
php artisan queue:work
```

## Working with forms

Get to [http://localhost:2124/dashboard](Dashboard) on the browser.


Then navigate to the form and upload some data, e. g. *https://medium.com/swlh/fun-with-python-3-hacking-instagram-giveaways-35e5b1d51670*
& *article.meteredContent*. After a while - like a ~10s or so, click **Load Crawl Data** button on the grid and results will pop up.

If you **see errors**, please refer to *FAQ* - logs need better permission management.

You can try with the next one - *https://pbrilius.medium.com/laravel-docker-conversation-violations-on-compose-instance-for-example-8914a6cc23a3?sk=143bc131cccb93c082bb14fcfcb2cd06* *article.meteredContent*.

Want to start with a fresh database?

```shell
docker container exec -it project-alna_backend-alna_1 /bin/bash
cd laravel.app
php artisan migrate:fresh
```

then click **Load Crawl Data**.

# FAQ

* Cannot append to log file - `sudo chmod -Rv 2777 {backend,frontend}-alna/storage/logs`