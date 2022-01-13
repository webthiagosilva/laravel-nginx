FROM php:8-fpm

ARG user
ARG uid

RUN apt-get update && apt-get install -y \
    nano \    
    git \
    curl \
    zip \
    unzip \
    libpng-dev \
    libonig-dev \
    libxml2-dev 

RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install pdo pdo_mysql mbstring exif pcntl bcmath gd

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN useradd -G www-data,root -u $uid -d /home/$user $user
RUN mkdir -p /home/$user/.composer && \
    chown -R $user:$user /home/$user


RUN mkdir -p /usr/src/php/ext/redis \
    && curl -L https://github.com/phpredis/phpredis/archive/5.3.4.tar.gz | tar xvz -C /usr/src/php/ext/redis --strip 1 \
    && echo 'redis' >> /usr/src/php-available-exts \
    && docker-php-ext-install redis


WORKDIR /var/www/html


CMD ["php-fpm", "-y", "/usr/local/etc/php-fpm.conf", "-R"]


# MacOS staff group's gid is 20, so is the dialout group in alpine linux. We're not using it, let's just remove it.
#RUN delgroup dialout

#RUN addgroup -g $uid --system laravel
#RUN adduser -G laravel --system -D -s /bin/sh -u $user laravel

##RUN sed -i "s/user = www-data/user = laravel/g" /usr/local/etc/php-fpm.d/www.conf
#RUN sed -i "s/group = www-data/group = laravel/g" /usr/local/etc/php-fpm.d/www.conf
#RUN echo "php_admin_flag[log_errors] = on" >> /usr/local/etc/php-fpm.d/www.conf



