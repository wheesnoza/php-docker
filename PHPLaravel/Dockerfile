FROM php:8.3-fpm

ARG UID=1000
ARG UNAME=laravel
ARG GID=1000
ARG GNAME=laravel
ARG WORKDIR=/laravel

RUN apt-get update
RUN apt-get install -y curl zip unzip git libpng-dev libjpeg-dev libfreetype6-dev libonig-dev libzip-dev
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install -j$(nproc) gd mbstring zip pdo pdo_mysql

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash -
RUN apt-get install -y nodejs
RUN npm install -g npm@latest
RUN npm install -g create-vite

RUN groupadd -g $GID $GNAME
RUN useradd -u $UID -g $GNAME -m $UNAME

WORKDIR $WORKDIR
RUN chown -R $UNAME:$GNAME $WORKDIR

USER $UNAME

CMD ["php", "-a"]