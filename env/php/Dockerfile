FROM php:8.2-fpm

# Instalamos las dependencias necesarias
RUN apt-get update && pecl install apcu uploadprogress && apt-get install -y \
    build-essential \
    libzip-dev \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libonig-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    git \
    curl

# Instalamos extensiones de PHP
RUN docker-php-ext-install pdo_mysql zip exif pcntl
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install gd
RUN docker-php-ext-enable apcu uploadprogress

# Instalamos composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Instalamos nodejs
RUN rm -rf /var/lib/apt/lists/ && curl -sL https://deb.nodesource.com/setup_20.x | bash -
RUN apt-get install nodejs -y


# Nos movemos a /var/www/
WORKDIR /var/www/html

# Exponemos el puerto 9000 a la network
EXPOSE 9000

# Corremos el comando php-fpm para ejecutar PHP
CMD ["php-fpm"]