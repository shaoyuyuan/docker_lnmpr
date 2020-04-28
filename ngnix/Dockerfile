#base images
FROM centos7:v1

#MAINTAINER
MAINTAINER 305400706@qq.com

# set time
ENV TIME_ZOME Asia/Shanghai

#COPY nginx-1.9.9.tar.gz /opt/nginx-1.9.9.tar.gz

#nginx

#cd /opt
WORKDIR /opt

RUN wget http://nginx.org/download/nginx-1.9.9.tar.gz  \
    && tar -xzf nginx-1.9.9.tar.gz \
    && cd /opt/nginx-1.9.9 \
    && ./configure  --prefix=/usr/local/nginx  --with-http_ssl_module --with-http_sub_module --with-http_dav_module --with-http_flv_module  --with-http_gzip_static_module --with-http_stub_status_module --with-debug \
    && make && make install

#cd /nginx
WORKDIR /syy/docker/nginx

#nginx.conf
COPY nginx.conf /usr/local/nginx/conf/nginx.conf
COPY vhost/* /usr/local/nginx/conf/vhost/
EXPOSE 80 443

#start nginx
ENTRYPOINT ["/usr/local/nginx/sbin/nginx", "-g", "daemon off;"]
