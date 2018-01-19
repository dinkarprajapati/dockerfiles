# UBUNTU SERVER WITH PHP 5.6 AND APACHE 2.4
FROM ubuntu:latest

RUN apt-get update \
	&& apt-get install -y apache2 \
	&& apt-get install -y software-properties-common \
	&& apt-get install -y language-pack-en-base \
	&& LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php

RUN mkdir /app
WORKDIR /var/www/html

RUN apt-get update && apt-get install -y \
	bzip2 \
	ca-certificates \
	curl \
	dpkg-dev \
	gcc \
	liblua5.2-dev \
	libpcre++-dev \
	libxml2-dev \
	make \
	man \
	vim \
	wget \
	sudo \
	zlib1g-dev \
	&& rm -rf /var/lib/apt/lists/*

RUN a2enmod rewrite

RUN apt-get update && apt-get install -y php5.6

RUN requirements="libapache2-mod-php5.6 php5.6 php5.6-bcmath php5.6-common php5.6-curl php5.6-gd php5.6-iconv php5.6-imagick php5.6-intl php5.6-mbstring php5.6-mcrypt php5.6-mysql php5.6-soap php5.6-xsl php5.6-zip" \
	&& apt-get install -y --no-install-recommends $requirements \
	&& rm -rf /var/lib/apt/lists/*

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

RUN curl -sL https://deb.nodesource.com/setup_9.x | sudo -E bash - \
	&& apt-get install -y nodejs

COPY ./configfiles/000-default.conf /etc/apache2/sites-available/000-default.conf
COPY ./configfiles/apache2.conf /etc/apache2/apache2.conf
COPY ./configfiles/ports.conf /etc/apache2/ports.conf

LABEL maintainer="Dinkar Prajapati <pradino@gmail.com>" \
	version="1.0"

EXPOSE 80
CMD /usr/sbin/apache2ctl -D FOREGROUND