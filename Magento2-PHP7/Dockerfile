FROM ubuntu:latest

RUN apt-get update \
	&& apt-get install -y apache2 \
	&& apt-get install -y software-properties-common \
	&& apt-get install -y language-pack-en-base \
	&& LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php

RUN mkdir /app
WORKDIR /var/www/html

COPY ./configfiles/000-default.conf /etc/apache2/sites-available/000-default.conf
COPY ./configfiles/apache2.conf /etc/apache2/apache2.conf

ENV NGHTTP2_VERSION 1.7.1-1

RUN apt-get update && apt-get install -y \
	bzip2 \
	ca-certificates \
	dpkg-dev \
	gcc \
	liblua5.2-dev \
	libnghttp2-dev=$NGHTTP2_VERSION \
	libpcre++-dev \
	libxml2-dev \
	make \
	man \
	vim \
	wget \
	zlib1g-dev \
	&& rm -rf /var/lib/apt/lists/*

RUN a2enmod rewrite

RUN apt-get update && apt-get install -y php7.1

RUN requirements="libapache2-mod-php7.1 php7.1 php7.1-bcmath php7.1-common php7.1-curl php7.1-gd php7.1-iconv php7.1-intl php7.1-mbstring php7.1-mcrypt php7.1-mysql php7.1-soap php7.1-xsl php7.1-zip" \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends $requirements \
	&& rm -rf /var/lib/apt/lists/*

# RUN echo "memory_limit=1024M" > /etc/php/7.1/apache2/php.ini

# RUN apt-get install -y mysql-server mysql-client

LABEL maintainer="Dinkar Prajapati <pradino@gmail.com>" \
	version="1.0"

EXPOSE 80
CMD /usr/sbin/apache2ctl -D FOREGROUND