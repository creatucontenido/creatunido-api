# Usa la imagen base de PHP 8.3
FROM php:8.3-fpm

# Instala las dependencias necesarias
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    git \
    curl \
    iputils-ping \
    htop

RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install pdo pdo_mysql gd mbstring exif pcntl bcmath opcache

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer 


# Install Xdebug y phpredis
RUN pecl install xdebug redis \
    && docker-php-ext-enable xdebug redis

# Configure Xdebug para desarrollo
COPY ./conf.d/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

# Copy additional php config if required
COPY ./conf.d/php.ini /usr/local/etc/php/conf.d/php.ini

