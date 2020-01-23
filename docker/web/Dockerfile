FROM    amazonlinux:2016.09
MAINTAINER Ngo Van Thang <thangnvbkhn@gmail.com>

# Set TERM env to avoid error message "TERM environment variable not set" when running from inside the container
#ENV TERM=xterm
ENV LANG=C.UTF-8
ENV APP_HOME=/data/www
ENV ENTRYKIT_VERSION=0.4.0

WORKDIR /tmp

RUN     cp -p /usr/share/zoneinfo/Japan /etc/localtime

# Install common packages
RUN     yum install -y \
				wget \
        git \
        mysql \
        php72 php72-mbstring php72-zip php72-pdo php72-mysqli php72-devel php72-pecl-imagick php72-gmp php72-bcmath php72-gd

COPY    httpd.conf /etc/httpd/conf/httpd.conf
COPY    php.ini /etc/php.ini

RUN wget https://github.com/progrium/entrykit/releases/download/v0.4.0/entrykit_0.4.0_Linux_x86_64.tgz && \
    tar -xvzf entrykit_0.4.0_Linux_x86_64.tgz && \
    rm entrykit_0.4.0_Linux_x86_64.tgz && \
    mv entrykit /bin/entrykit && \
    chmod +x /bin/entrykit && \
    entrykit --symlink

# Docker側でlistenするポート番号を指定
EXPOSE  80 22 443

WORKDIR $APP_HOME