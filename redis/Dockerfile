#base images
FROM centos7:v1

#MAINTAINER
MAINTAINER 305400706@qq.com

# set time
ENV TIME_ZOME Asia/Shanghai


#cd /opt
WORKDIR /opt

RUN wget http://download.redis.io/releases/redis-5.0.8.tar.gz  \
    && tar -zxvf redis-5.0.8.tar.gz  \
    && cd redis-5.0.8  \
    && make &&  make install

ADD redis.conf /etc/redis.conf

EXPOSE 6379

VOLUME ["/data"]

WORKDIR /data

CMD "/usr/local/bin/redis-server" "/etc/redis.conf"
#ENTRYPOINT ["/usr/local/bin/redis-server", "-F", "-c", "/etc/redis.conf"] 