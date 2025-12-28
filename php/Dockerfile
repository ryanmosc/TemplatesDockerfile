FROM php:8.3-apache

WORKDIR /app

RUN docker-php-ext-install pdo pdo_mysql

WORKDIR /var/www/html

COPY . .

EXPOSE 80