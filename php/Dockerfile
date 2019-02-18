FROM php:5.6-fpm-alpine

RUN apk add shadow && usermod -u 1000 www-data && groupmod -g 1000 www-data \
    && apk add --no-cache bash freetype libpng libjpeg-turbo freetype-dev libpng-dev libjpeg-turbo-dev \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && docker-php-ext-configure gd \
        --with-gd \
        --with-freetype-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ \
    && NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
    && docker-php-ext-install -j${NPROC} gd iconv mbstring mysql mysqli pdo pdo_mysql \
    && apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev