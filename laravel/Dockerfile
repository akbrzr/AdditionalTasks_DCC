FROM php:8.2-fpm-alpine AS builder

WORKDIR /app

RUN apk add --no-cache git curl
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY . /app

RUN mkdir -p /app/storage /app/bootstrap/cache && \
    chmod -R 777 /app/storage /app/bootstrap/cache

RUN composer install --no-dev --no-interaction --prefer-dist --optimize-autoloader

FROM php:8.2-fpm-alpine

WORKDIR /var/www

RUN apk add --no-cache nginx

COPY --from=builder /app /var/www

COPY docker/nginx.conf /etc/nginx/conf.d/default.conf

RUN chown -R www-data:www-data /var/www/storage /var/www/bootstrap/cache && \
    chmod -R 775 /var/www/storage /var/www/bootstrap/cache

EXPOSE 9000

CMD ["php-fpm"]
