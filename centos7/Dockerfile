#base images
FROM centos:centos7

#MAINTAINER
MAINTAINER 305400706@qq.com

# set time
ENV TIME_ZOME Asia/Shanghai

#add wget
RUN yum update -y \
    && yum install -y epel-release \
    && yum install -y wget \
    && yum install -y bzip2 \
    && cd /etc/yum.repos.d \
    && mv CentOS-Base.repo CentOS-Base.repo.back \
    && wget -P /etc/yum.repos.d/ http://mirrors.aliyun.com/repo/Centos-7.repo \
    && wget -P /etc/yum.repos.d/ http://mirrors.163.com/.help/CentOS7-Base-163.repo \
    && yum makecache  \
    && yum -y install  gcc gcc-c++ autoconf automake make zlib zlib-devel net-tools openssl* pcre* wget \
    && yum clean all  && rm -rf /var/cache/yum/*