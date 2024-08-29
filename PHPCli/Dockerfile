FROM php:8.3-cli

RUN apt-get update
RUN apt-get install -y git curl

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

ARG UID=1000
ARG GID=1000
RUN groupadd -g $GID www
RUN useradd -u $UID -g www -m www

WORKDIR /app
RUN chown -R www:www /app

USER www

CMD ["php", "-a"]