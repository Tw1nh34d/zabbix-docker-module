# https://github.com/monitoringartist/zabbix-docker-monitoring

# Define required CentOS version by using FROM tag. Avalaible: centos7/centos6/...
FROM centos:7

MAINTAINER "Jan Garaj" <info@monitoringartist.com>

# Define required Zabbix version (<version>) or release (release/<version>), e.g. 4.2.2, or release/4.2  
ENV ZABBIX_VERSION=4.4.4

WORKDIR /root

RUN \
   yum -y -q install git automake autoconf gcc make pcre-devel 1>/dev/null && \
   git clone -q https://github.com/monitoringartist/zabbix-docker-monitoring

RUN \
   git clone -b ${ZABBIX_VERSION} --depth 1 https://github.com/zabbix/zabbix.git ~/zabbix && \
   cd ~/zabbix/ && \
   ./bootstrap.sh 1>/dev/null && \
   ./configure --enable-agent 1>/dev/null && \
   cp -R ~/zabbix-docker-monitoring/src/modules/zabbix_module_docker/ ~/zabbix/src/modules/ && \
   cd ~/zabbix/src/modules/zabbix_module_docker && \
   make

## Dockerized compilation (build from remote URL or local PATH):
# docker build --rm=true -t local/zabbix-docker-module-compilation https://github.com/monitoringartist/zabbix-docker-monitoring.git#master:dockerfiles/centos/
# docker build --rm=true -t local/zabbix-docker-module-compilation .
# docker run --rm -v /tmp:/tmp local/zabbix-docker-module-compilation cp /root/zabbix/src/modules/zabbix_module_docker/zabbix_module_docker.so /tmp/zabbix_module_docker.so
# docker rmi -f local/zabbix-docker-module-compilation
## use/copy /tmp/zabbix_module_docker.so in your Zabbix
# usermod -aG docker zabbix