# -----------------------------
# Laravel PHP-FPM Dockerfile
# -----------------------------

FROM php:8.3-fpm-alpine

# -----------------------------
# System Packages + PHP Extensions
# -----------------------------
RUN apk add --no-cache bash git unzip libzip-dev oniguruma-dev mysql-client curl \
    && docker-php-ext-install pdo_mysql mbstring zip bcmath

# -----------------------------
# Composer installieren
# -----------------------------
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# -----------------------------
# Arbeitsverzeichnis
# -----------------------------
WORKDIR /var/www

# -----------------------------
# Laravel App kopieren
# -----------------------------
COPY . /var/www

# -----------------------------
# Storage + Cache erstellen & Rechte setzen
# -----------------------------
RUN mkdir -p /var/www/storage/framework /var/www/storage/logs /var/www/bootstrap/cache \
    && chown -R www-data:www-data /var/www/storage /var/www/bootstrap/cache \
    && chmod -R 775 /var/www/storage /var/www/bootstrap/cache

# -----------------------------
# Optional: Composer Abhängigkeiten installieren
# -----------------------------
# Falls du willst, kannst du direkt beim Build dependencies installieren:
# RUN composer install --no-dev --optimize-autoloader

# -----------------------------
# Benutzer setzen
# -----------------------------
USER www-data

# -----------------------------
# Expose PHP-FPM Port
# -----------------------------
EXPOSE 9000

# -----------------------------
# Start PHP-FPM
# -----------------------------
CMD ["php-fpm"]
