FROM ubuntu:18.04

LABEL Maintainer="Dylan Ngo" \
      Description="ProxySQL"

RUN apt-get update \
    && apt-get install -y vim \
    && apt-get install -y htop \
    && apt-get install -y mysql-server \
    && apt-get install -y wget

RUN wget https://github.com/sysown/proxysql/releases/download/v2.0.2/proxysql_2.0.2-ubuntu16_amd64.deb \
    && dpkg -i proxysql_2.0.2-ubuntu16_amd64.deb

CMD ["/usr/bin/proxysql","-f","-c","/etc/proxysql.cnf"]