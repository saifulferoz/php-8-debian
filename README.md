# PHP 8.3 Debian Multi-Arch Docker Image (`ferozcse/php-8.3-debian`)

[![Docker Pulls](https://img.shields.io/docker/pulls/ferozcse/php-8.3-debian.svg?style=flat-square)](https://hub.docker.com/r/ferozcse/php-8.3-debian)
[![Docker Stars](https://img.shields.io/docker/stars/ferozcse/php-8.3-debian.svg?style=flat-square)](https://hub.docker.com/r/ferozcse/php-8.3-debian)
[![PHP Version](https://img.shields.io/badge/PHP-8.3.37-777BB4.svg?style=flat-square&logo=php&logoColor=white)](https://www.php.net)
[![Debian Version](https://img.shields.io/badge/Debian-12%20(Bookworm)-D70A53.svg?style=flat-square&logo=debian&logoColor=white)](https://www.debian.org)
[![Architectures](https://img.shields.io/badge/Architectures-linux%2Famd64%20%7C%20linux%2Farm64-blue.svg?style=flat-square&logo=docker&logoColor=white)](https://hub.docker.com/r/ferozcse/php-8.3-debian)
[![License](https://img.shields.io/badge/License-MIT-green.svg?style=flat-square)](LICENSE)

Production-ready, highly optimized, enterprise-grade Docker image for **PHP 8.3 (8.3.37)** based on **Debian 12 (Bookworm)** with full multi-architecture support (**`linux/amd64`** and **`linux/arm64`**).

Designed specifically for modern PHP microservices, high-traffic Laravel/Symfony APIs, distributed tracing (Elastic APM), background queue workers, and document/report generation pipelines.

---

## 📌 Quick Reference

- **Docker Hub Repository**: [`ferozcse/php-8.3-debian`](https://hub.docker.com/r/ferozcse/php-8.3-debian)
- **Source Repositories**:
  - [saifulferoz/php-8.2-buster](https://github.com/saifulferoz/php-8.2-buster) (Build automation, multi-arch scripts, and Dockerfiles)
  - [saifulferoz/php-8-debian](https://github.com/saifulferoz/php-8-debian/tree/8.3.x) (`8.3.x` branch)
- **Author & Maintainer**: Saiful Islam Feroz ([@saifulferoz](https://github.com/saifulferoz), [ferozcse@gmail.com](mailto:ferozcse@gmail.com))
- **Base OS**: Debian 12 (Bookworm) Slim
- **Supported Platforms**: `linux/amd64` (x86_64), `linux/arm64` (Apple Silicon M-series, AWS Graviton, Ampere)

---

## 🏷️ Supported Image Variants & Tags

All variants provide native multi-architecture manifest lists covering both `linux/amd64` and `linux/arm64`:

| Variant | Tag Convention | Purpose & Key Features |
| :--- | :--- | :--- |
| **`fpm`** *(Default)* | `latest`, `fpm`, `fpm-8.3`, `fpm-8.3.37` | High-performance PHP-FPM configured for Nginx, Caddy, or Traefik. Tuned with high worker limits (`rlimit_files=131072`, `request_terminate_timeout=300`). |
| **`fpm-apm`** | `fpm-apm`, `fpm-apm-8.3`, `fpm-apm-8.3.37` | PHP-FPM with the official **Elastic APM PHP Agent** (`elastic_apm` v1.17.1) pre-installed and enabled for distributed tracing. |
| **`cli`** | `cli`, `cli-8.3`, `cli-8.3.37`, `cli-amd64` | CLI runner for Composer tasks, Artisan commands, database migrations, and scheduled cron jobs. Includes **Node.js (18.x/20.x)**, **npm**, and **Xdebug**. |
| **`supervisor`** | `supervisor`, `supervisor-8.3`, `supervisor-8.3.37`, `supervisor-amd64` | CLI base with **Supervisord** configured as the container entrypoint. Purpose-built for running persistent Laravel Queue workers, Horizon, and background daemons. |
| **`apache`** | `apache`, `apache-8.3`, `apache-8.3.37` | Apache 2.4 MPM Prefork with `mod_rewrite`, `mod_headers`, and DocumentRoot configured to `/var/www/public`. |
| **`dev`** | `dev`, `dev-8.3`, `dev-8.3.37` | Development environment bundling Apache, full development packages, and **Xdebug** pre-configured for remote IDE step-debugging. |

---

## 🧩 Included PHP Extensions & Drivers

Every variant is built with an extensive suite of compiled extensions to support diverse enterprise backends out-of-the-box without requiring custom compilation:

### 1. Database & Cache Drivers
- **`oci8` & Oracle Instant Client**: Includes Oracle Instant Client basiclite and SDK with dynamic runtime linker configuration (`ldconfig`). Connect to Oracle Database without extra client installation.
- **`pdo_mysql` & `mysqli`**: MySQL 8.x / MariaDB relational database connectivity.
- **`pdo_pgsql` & `pgsql`**: PostgreSQL driver with native `libpq-dev`.
- **`mongodb`**: Official MongoDB extension for document stores.
- **`redis`**: High-throughput Redis caching and session management.
- **`amqp`**: RabbitMQ message broker integration via `librabbitmq-dev`.

### 2. Performance, Caching & Serialization
- **`opcache`**: Pre-configured Zend OPcache with CLI optimization (`opcache.enable_cli=1`).
- **`apcu`**: In-memory APC user cache for local key-value storage.
- **`igbinary`**: Compact binary serializer for high-speed Redis session and cache storage.
- **`yaml`**: High-performance YAML parser based on LibYAML.

### 3. Core & Business Utilities
- **`intl`**: Internationalization and localization support (ICU library).
- **`zip`**: Full Zip archive manipulation via `libzip-dev`.
- **`soap` & `xsl`**: SOAP web services and XML transformations via `libxslt`.
- **`bcmath`**: Arbitrary precision mathematics for financial systems.
- **`exif` & `gettext`**: Image metadata inspection and multilingual translations.
- **`sockets` & `iconv`**: Low-level networking and character encoding conversions.

### 4. Graphics & PDF Generation
- **`gd`**: Compiled with FreeType, JPEG, and PNG format support.
- **`imagick`**: ImageMagick 6 / MagickWand support for raster and vector graphics.
- **`wkhtmltopdf` (v0.12.6.1-3)**: Headless WebKit HTML-to-PDF command-line utility.
- **`merge2pdf` (v1.1.0)**: High-speed native PDF merger.
- **Included Fonts**:
  - `ttf-mscorefonts-installer` (Arial, Times New Roman, Verdana, Georgia)
  - Arial Narrow font family
  - **SolaimanLipi** Unicode font for complex Bengali text rendering
  - Fontconfig and X11 font caches (`fc-cache`) pre-generated.

### 5. Developer & APM Tooling
- **Composer**: Latest multi-stage release (`/usr/bin/composer`) with `COMPOSER_ALLOW_SUPERUSER=1`.
- **Node.js & npm**: Bundled in `cli` variant for compiling frontend assets (Vite/Mix) and CLI tools.
- **Xdebug**: Pre-installed and ready in `dev` and `cli` variants.
- **Elastic APM**: Bundled in `fpm-apm` for distributed telemetry in Elasticsearch / Kibana.

---

## ⚙️ Standard PHP Runtime Configuration

All variants ship with sensible production defaults located at `/usr/local/etc/php/conf.d/00-override.ini`:

```ini
; Timezone
date.timezone = Asia/Dhaka

; Uploads & Resource Limits
upload_max_filesize = 256M
post_max_size = 2048M
max_input_vars = 10000
memory_limit = 3504M
max_execution_time = 300
expose_php = Off

; OPcache
opcache.enable = 1
opcache.enable_cli = 1
opcache.validate_timestamps = 1
opcache.revalidate_freq = 0

; Logging
error_reporting = 4339
display_errors = Off
display_startup_errors = Off
log_errors = On
error_log = /dev/stderr
log_errors_max_len = 1024
ignore_repeated_errors = On
html_errors = Off
```

---

## 🚀 Quickstart & Usage Examples

### 1. PHP-FPM with Nginx (`fpm` variant)

```dockerfile
# Dockerfile
FROM ferozcse/php-8.3-debian:fpm

WORKDIR /var/www

# Copy application files
COPY --chown=www-data:www-data . /var/www

# Install production dependencies
RUN composer install --no-dev --optimize-autoloader --no-interaction

USER www-data

EXPOSE 9000
CMD ["php-fpm"]
```

Sample `docker-compose.yml`:
```yaml
services:
  app:
    image: ferozcse/php-8.3-debian:fpm
    volumes:
      - ./:/var/www
    environment:
      APP_ENV: production
      DB_HOST: mysql

  web:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./:/var/www
      - ./nginx.conf:/etc/nginx/conf.d/default.conf:ro
    depends_on:
      - app
```

---

### 2. Distributed Tracing with Elastic APM (`fpm-apm` variant)

```yaml
services:
  api:
    image: ferozcse/php-8.3-debian:fpm-apm
    environment:
      ELASTIC_APM_SERVER_URL: "http://apm-server:8200"
      ELASTIC_APM_SERVICE_NAME: "billing-api"
      ELASTIC_APM_ENVIRONMENT: "production"
      ELASTIC_APM_SECRET_TOKEN: "your_apm_token"
      ELASTIC_APM_TRANSACTION_SAMPLE_RATE: "1.0"
    volumes:
      - ./:/var/www
    ports:
      - "9000:9000"
```

---

### 3. Background Queue Worker with Supervisord (`supervisor` variant)

```dockerfile
# Dockerfile
FROM ferozcse/php-8.3-debian:supervisor

# Copy custom supervisor worker config into conf.d
COPY ./docker/worker.conf /etc/supervisor/conf.d/worker.conf

WORKDIR /var/www
COPY . /var/www

CMD ["-c", "/etc/supervisor/supervisord.conf", "-n"]
```

Sample `/etc/supervisor/conf.d/worker.conf`:
```ini
[program:laravel-worker]
process_name=%(program_name)s_%(process_num)02d
command=php /var/www/artisan queue:work redis --sleep=3 --tries=3 --max-time=3600
autostart=true
autorestart=true
stopasgroup=true
killasgroup=true
user=www-data
numprocs=4
redirect_stderr=true
stdout_logfile=/dev/stdout
stdout_logfile_maxbytes=0
```

---

### 4. Running Migrations or One-off Commands (`cli` variant)

```bash
# Run composer install
docker run --rm -v $(pwd):/app -w /app ferozcse/php-8.3-debian:cli composer install

# Run database migrations
docker run --rm --network app-net -v $(pwd):/app -w /app ferozcse/php-8.3-debian:cli php artisan migrate --force

# Run interactive bash
docker run --rm -it ferozcse/php-8.3-debian:cli bash
```

---

## 🏗️ Architecture & Multi-Platform Verification

All tags are published as multi-architecture manifest lists combining:
- **`linux/amd64`**: x86_64 servers, Intel/AMD workstations, standard Cloud VMs.
- **`linux/arm64`**: Apple Silicon (M1/M2/M3/M4), AWS Graviton instances, Raspberry Pi 4/5.

Verify image architecture with:
```bash
docker buildx imagetools inspect ferozcse/php-8.3-debian:fpm-8.3.37
```

---

## 📜 License & Author

- **Maintained by**: Saiful Islam Feroz ([ferozcse@gmail.com](mailto:ferozcse@gmail.com))
- **GitHub**: [@saifulferoz](https://github.com/saifulferoz)
- **License**: MIT
