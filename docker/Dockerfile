FROM centos:7

RUN rpm --import /etc/pki/rpm-gpg/RPM*
RUN rpm --import https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7
RUN rm -rf /etc/localtime && ln -s /usr/share/zoneinfo/Asia/Taipei /etc/localtime

RUN yum update -y && yum clean all && yum install -y epel-release && \
    yum install -y nginx supervisor acl wget tar autoconf git zip unzip && \
    yum install -y libxml2-devel openssl-devel && \
    yum install -y curl-devel libuuid-devel.x86_64 && \
    yum install -y glibc-headers gcc-c++ make && \
    yum install -y python34 python34-jinja2 && \
    yum install -y re2c icu libicu libicu-devel && \
    yum reinstall -y glibc-common && \
    yum clean all

RUN wget http://php.net/distributions/php-7.2.10.tar.gz
RUN tar -C . -zxf php-7.2.10.tar.gz
WORKDIR php-7.2.10
RUN ./configure --prefix=/usr/local/web/php \
                --with-libdir=lib64 \
                --enable-fpm --with-fpm-user=nobody --with-fpm-group=nobody \
                --with-config-file-path=/etc \
                --enable-mbstring \
                --with-openssl=shared \
                --with-libxml-dir=/usr/lib \
                --with-curl=shared \
                --enable-sockets \
                --with-zlib --with-iconv --with-gettext \
                --enable-intl --enable-bcmath=shared --enable-mysqlnd=shared --with-pdo-mysql=shared && \
    make && make install

RUN ln -s /usr/local/web/php/sbin/* /usr/local/sbin/
RUN ln -s /usr/local/web/php/bin/* /usr/local/bin/

WORKDIR /

RUN rm -rf php-7.2.10*
