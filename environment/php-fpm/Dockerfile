FROM php:8.1-fpm-buster

# Set working directory
WORKDIR /web
# Install system dependencies
RUN BUILD_DEPS=" \
        libpq-dev \
        libncurses5-dev \
        zlib1g-dev \
        libicu-dev \
        libpng-dev \
        libonig-dev \
        libxml2-dev \
    " \
    && apt-get update -q \
    && apt-get install -y --no-install-recommends git curl zip unzip ssh  \
      ${BUILD_DEPS} \
    # Install PHP extensions
    && docker-php-ext-install \
            pdo_mysql \
            mbstring \
            exif \
            pcntl \
            bcmath \
            gd\
            sockets \
    && docker-php-source delete \
    && apt-get purge -y ${BUILD_DEPS} \
    # Clear cache
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \


    # Get latest Composer
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && mkdir -m 777 /.composer \
    && php -- --install-dir=/usr/local/bin --filename=composer
