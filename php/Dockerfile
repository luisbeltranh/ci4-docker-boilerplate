# Usamos una imagen oficial de PHP con Apache
FROM php:8.1-apache

# Instalamos las dependencias necesarias para las extensiones de PHP
RUN apt-get update && apt-get install -y \
    libicu-dev \
    libzip-dev \
    unzip \
    git \
    && rm -rf /var/lib/apt/lists/*

# Instalamos las extensiones de PHP para CodeIgniter 4 y MySQL
RUN docker-php-ext-install \
    intl \
    pdo_mysql \
    mysqli \
    zip

# Habilitamos el módulo rewrite de Apache para las URLs amigables de CodeIgniter
RUN a2enmod rewrite

# Instalamos Composer (el manejador de paquetes de PHP)
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Establecemos el directorio de trabajo
WORKDIR /var/www/html