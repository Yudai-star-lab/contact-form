FROM php:8.2-fpm

COPY php.ini /usr/local/etc/php/

ARG UID=1000
ARG GID=1000

RUN groupadd -g ${GID} appgroup \
  && useradd -u ${UID} -g appgroup -m appuser

RUN apt update \
  && apt install -y default-mysql-client zlib1g-dev libzip-dev unzip \
  && docker-php-ext-install pdo_mysql zip

RUN curl -sS https://getcomposer.org/installer | php \
  && mv composer.phar /usr/local/bin/composer \
  && composer self-update

# ★ これがないと create-project が永遠に失敗します
ENV HOME=/home/appuser

WORKDIR /var/www

USER appuser

CMD ["php-fpm"]