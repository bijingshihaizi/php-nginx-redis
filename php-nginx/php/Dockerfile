FROM php:7.2-fpm

ENV PHPREDIS_VERSION 4.0.0
# 阿里云源
RUN /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo 'Asia/Shanghai' > /etc/timezone \
    && echo "deb http://mirrors.aliyun.com/debian/ buster main non-free contrib \
\ndeb-src http://mirrors.aliyun.com/debian/ buster main non-free contrib \
\ndeb http://mirrors.aliyun.com/debian-security buster/updates main \
\ndeb-src http://mirrors.aliyun.com/debian-security buster/updates main \
\ndeb http://mirrors.aliyun.com/debian/ buster-updates main non-free contrib \
\ndeb-src http://mirrors.aliyun.com/debian/ buster-updates main non-free contrib \
\ndeb http://mirrors.aliyun.com/debian/ buster-backports main non-free contrib \
\ndeb-src http://mirrors.aliyun.com/debian/ buster-backports main non-free contrib">/etc/apt/sources.list

# 中科大源
# RUN /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
#     && echo 'Asia/Shanghai' > /etc/timezone \
#     && echo "">/etc/apt/sources.list \
#     && echo "deb http://mirrors.ustc.edu.cn/debian stable main contrib non-free \
#     \ndeb http://mirrors.ustc.edu.cn/debian stable-updates main contrib non-free" > /etc/apt/sources.list

# Libs
RUN apt-get update \
    && apt-get install -y \
        curl \
        wget \
        git \
        zip \
        libz-dev \
        libssl-dev \
        libnghttp2-dev \
        libpcre3-dev \
        libpng-dev \
        libjpeg-dev \
        gawk \
        uuid-dev \
        libmcrypt-dev \
        vim \
        bash \
        openssl\
        libzip-dev \
    openssh-server \
    && apt-get clean \
    && apt-get autoremove

# Redis extension
RUN wget http://pecl.php.net/get/redis-${PHPREDIS_VERSION}.tgz -O /tmp/redis.tar.tgz \
    && pecl install /tmp/redis.tar.tgz \
    && rm -rf /tmp/redis.tar.tgz \
    && docker-php-ext-enable redis

RUN docker-php-ext-install mysqli pdo_mysql && docker-php-ext-enable mysqli pdo_mysql
