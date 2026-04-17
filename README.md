# Laravel Project Setup

## Prerequisites

* PHP >= 8.2
* Composer
* Docker Desktop (for Laravel Sail)

La base de datos del proyecto se creó en MySQL dentro de Docker, usando un contenedor similar a este:

```bash
docker run -d \
	--name mysql_laravel \
	-e MYSQL_ROOT_PASSWORD=root \
	-e MYSQL_DATABASE=laravel \
	-e MYSQL_USER=sail \
	-e MYSQL_PASSWORD=password \
	-p 3306:3306 \
	mysql:8.0
```

## Installation

1. **Clone the repository**
```bash
git clone https://github.com/alejandrorh97/instructoria
cd <project-folder>
```


2. **Install dependencies**
```bash
composer install
```


3. **Environment configuration**
```bash
cp .env.example .env
php artisan key:generate
php artisan jwt:secret
php artisan config:clear
php artisan cache:clear
```


4. **Database migration**
```bash
php artisan migrate
```

La base de datos `laravel` ya queda creada dentro del contenedor MySQL de Docker.

> Important: the default `.env.example` is configured for local execution (`DB_HOST=127.0.0.1`).
> If you run commands inside Docker/Sail, use `DB_HOST=mysql`.

---

## Execution with Laravel Sail (Docker)

If you prefer using Docker, follow these steps:

1. **Start Sail**
```bash
./vendor/bin/sail up -d
```


2. **Generate app key via Sail (first run only)**
```bash
./vendor/bin/sail artisan key:generate
```


3. **Run migrations via Sail**
```bash
./vendor/bin/sail artisan migrate
```


4. **Access the application**
The app will be available at: `http://localhost:8080`
---

## Local Development (Without Docker)

1. **Use local DB values in `.env`**
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=sail
DB_PASSWORD=password
```

2. **Generate JWT secret and clear cache**
```bash
php artisan jwt:secret
php artisan config:clear
php artisan cache:clear
```

3. **Install MySQL driver for PHP (pdo_mysql)**
On Ubuntu/Debian:
```bash
sudo apt install php-mysql
```

4. **Run migrations**
```bash
php artisan migrate
```

5. **Serve the application**
```bash
php artisan serve
```

## Common Error

If you get:

`could not find driver (Connection: mysql, Host: mysql, Port: 3306...)`

It usually means one of these:

1. You ran `php artisan ...` locally, but `.env` still has `DB_HOST=mysql` (Docker hostname).
2. Your local PHP does not have `pdo_mysql` installed.

If you are using Docker/Sail, run commands with `./vendor/bin/sail artisan ...`.
