FROM php:8.3-fpm-bullseye

# Install dependencies we need
RUN mkdir -p /usr/share/man/man1 /usr/share/man/man7 \
	&& apt -y update && apt-get install -y \
	gnupg2 \
	&& apt-get update && apt-get install -y \
	bzip2 \
	default-mysql-client \
	exiftool \
	git-core \
	imagemagick \
	libbz2-dev \
	libc-client-dev \
	libfreetype6-dev \
	libicu-dev \
	libjpeg62-turbo-dev \
	libkrb5-dev \
	libldap2-dev \
	libmagickwand-dev \
	libmemcached-dev \
	libpng-dev \
	libpq-dev \
	libssl-dev \
	libwebp-dev \
	libxml2-dev \
	libzip-dev \
	libonig-dev \
	openssl \
	pv \
	jq \
	rsync \
	ssh \
	unzip \
	wget \
	subversion \
	xfonts-75dpi \
	xfonts-base \
	zlib1g-dev \
	&& pecl install apcu \
	&& pecl install memcached \
	&& pecl install oauth \
	&& pecl install redis-6.0.2 \
	&& pecl install xdebug-3.3.1 \
	&& docker-php-ext-configure ldap --with-libdir=lib/$(uname -m)-linux-gnu/ \
	&& docker-php-ext-enable apcu \
	&& docker-php-ext-enable memcached \
	&& docker-php-ext-enable oauth \
	&& docker-php-ext-enable redis \
	&& docker-php-ext-install bcmath \
	&& docker-php-ext-install bz2 \
	&& docker-php-ext-install calendar \
	&& docker-php-ext-install exif \
	&& docker-php-ext-install gettext \
	&& docker-php-ext-install intl \
	&& docker-php-ext-install ldap \
	&& docker-php-ext-install mbstring \
	&& docker-php-ext-install mysqli \
	&& docker-php-ext-install opcache \
	&& docker-php-ext-install pcntl \
	&& docker-php-ext-install pdo \
	&& docker-php-ext-install pdo_mysql \
	&& docker-php-ext-install pdo_pgsql \
	&& docker-php-ext-install soap \
	&& docker-php-ext-install zip \
	&& php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
	&& php composer-setup.php --install-dir=/usr/local/bin --filename=composer --version=2.2.22 \
	&& php -r "unlink('composer-setup.php');" \
	&& chsh -s /bin/bash www-data && mkdir -p /var/www/.composer && chown -R www-data:www-data /var/www \
	&& curl -sL https://raw.githubusercontent.com/axllent/mailpit/develop/install.sh | bash \
	&& apt-get -y clean \
	&& apt-get -y autoclean \
	&& apt-get -y autoremove \
	&& rm -rf /var/lib/apt/lists/* && rm -rf && rm -rf /var/lib/cache/* && rm -rf /var/lib/log/* && rm -rf /tmp/* \
	&& PHP_OPENSSL=yes docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
	&& docker-php-ext-install imap \
	&& docker-php-ext-configure gd --enable-gd --with-jpeg --with-webp --with-freetype \
	&& docker-php-ext-install gd

COPY ../../bin/xdebug.sh /usr/local/bin/xdebug
COPY ../../bin/wp-logs.sh /usr/local/bin/wp-logs
COPY ../../bin/setup-wordpress.sh /usr/local/bin/setup-wordpress

RUN chmod +x /usr/local/bin/xdebug
RUN chmod +x /usr/local/bin/wp-logs
RUN chmod +x /usr/local/bin/setup-wordpress

# Tests
RUN curl https://dl.yarnpkg.com
