# docker_lnmpr
dockerfile 部署lnmpr环境

### docker小白 参考https://github.com/Terry-Ye/docker-lnmpr  感谢原作者

# build
docker build -t centos/nginx:v1.12.1  ./nginx
docker build -t centos/mysql:v5.7   ./mysql
docker build -t centos/php:v7.0.12  ./php
docker build -t centos/redis:v3.2.6 ./redis

#备注：这里选取了172.172.0.0网段，也可以指定其他任意空闲的网段
docker network create --subnet=172.171.0.0/16 docker-at

# run

docker run --name mysql56  --restart=always  --net docker-at --ip 172.171.0.9 -d -p 3306:3306 -v /data/mysql:/var/lib/mysql -v /data/logs/mysql:/var/log/mysql -e MYSQL_ROOT_PASSWORD=root -it mysql:5.6


docker run --name redis5.0.8 --restart=always --net docker-at --ip 172.171.0.10 -d -p 6379:6379  -v /data/redis:/data -it redis:v5.0.8

docker run --name php7.2 --restart=always --net docker-at --ip 172.171.0.8 -d -p 9000:9000 -v /www:/www -v /data/php:/data --link mysql56:mysql56 --link redis5.0.8:redis5.0.8 -it php:v7.2.30 

docker run --name nginx1.9.9 --restart=always --net docker-at --ip 172.171.0.7 -p 80:80 -d -v /www:/www -v /data/nginx:/data --link php7.2:php7.2 -it nginx:v1.9.9 

# docker_lnmpr
