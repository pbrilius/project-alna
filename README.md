# project-alna

Install the submodule projects - `git submodule sync`. Then proceed with
virtual machines.

```
chmod -Rv o+rw backend-alna/storage
chmod -Rv o+rw frontend-alna/storage
```

Run launching up docker compose `docker-compose up -d`.

Install the assets
```
cd backend-alna;
composer install;
npm install;
cd ../frontend-alna;
composer install;
npm install;
npx tailwindcss init;
```

Run units:
```
cd frontend-alna
./vendor/bin/phpunit
```
