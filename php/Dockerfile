#base images
FROM centos7:v1

#MAINTAINER
MAINTAINER 305400706@qq.com

# set time
ENV TIME_ZOME Asia/Shanghai

#COPY php-7.2.30.tar.gz /opt/php-7.2.30.tar.gz
COPY redis-5.0.0.tgz /opt/redis-5.0.0.tgz
#COPY swoole-4.4.15.tgz /opt/swoole-4.4.15.tgz

#cd /opt
WORKDIR /opt

RUN yum -y install libxml2 libxml2-devel openssl openssl-devel libcurl libcurl-devel install libjpeg libjpeg-devel libpng libpng-devel freetype freetype-devel  \
    && yum clean all  && rm -rf /var/cache/yum/* \
    && wget https://www.php.net/distributions/php-7.2.30.tar.gz \
    && tar -xzf /opt/php-7.2.30.tar.gz \
    && cd /opt/php-7.2.30  \
    && ./configure   --prefix=/usr/local/php   --with-mysqli --with-pdo-mysql --with-iconv-dir --with-freetype-dir --with-jpeg-dir --with-png-dir --with-zlib --with-libxml-dir --enable-simplexml --enable-xml --disable-rpath --enable-bcmath --enable-soap --enable-zip --with-curl --enable-fpm --with-fpm-user=nobody --with-fpm-group=nobody --enable-mbstring --enable-sockets --with-mcrypt --with-gd --enable-gd-native-ttf --with-openssl --with-mhash --enable-opcache \
    && make &&  make install \
    && cd /opt \
    && tar -xzf redis-5.0.0.tgz \
    && cd /opt/redis-5.0.0  \
    && /usr/local/php/bin/phpize  \
    && ./configure --with-php-config=/usr/local/php/bin/php-config \
    && make \
    && make install \
    && cd /opt  \
    && wget https://pecl.php.net/get/swoole-4.4.15.tgz \
    && tar -xzf  swoole-4.4.15.tgz  \
    && cd swoole-4.4.15  \
    && /usr/local/php/bin/phpize   \
    && ./configure --with-php-config=/usr/local/php/bin/php-config  \
    && make &&  make install

ADD php-fpm.conf /usr/local/php/etc/php-fpm.conf 
ADD php.ini /usr/local/php/etc/php.ini
    
RUN cp /usr/local/php/etc/php-fpm.d/www.conf.default /usr/local/php/etc/php-fpm.d/www.conf

WORKDIR /www
EXPOSE 9000

VOLUME ["/www"]


#配置php
RUN sed -i -e 's/listen = 127.0.0.1:9000/listen = 9000/' /usr/local/php/etc/php-fpm.d/www.conf

#启动php
ENTRYPOINT ["/usr/local/php/sbin/php-fpm", "-F", "-c", "/usr/local/php/etc/php.ini"]