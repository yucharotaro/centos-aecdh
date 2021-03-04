FROM centos:7.8.2003

# 古い任意のバージョンのパッケージを入れるためcentos-releaseを更新
RUN yum update centos-release -y

RUN yum install -y \
    gcc \
    make \
    perl \
    zlib-devel \
    wget \
    vim \
    && rm -rf /var/cache/yum/* \
    && yum clean all

# 以下パッケージのインストール
# httpd/2.4.6-93.el7.centos
# openssl/1.0.2k-19.el7
RUN yum --disablerepo='*' --enablerepo=C7.8.2003-base install -y \
    httpd-2.4.6-93.el7.centos \
    openssl-1.0.2k-19.el7 \
    mod_ssl \
    && rm -rf /var/cache/yum/* \
    && yum clean all

RUN echo "NETWORKING=yes" > /etc/sysconfig/network

# 秘密鍵とサーバ証明書の設定
COPY ./ssl/server.key /etc/httpd/conf/
COPY ./ssl/server.crt /etc/httpd/conf/

RUN systemctl enable httpd

