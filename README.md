# zabbix-docker-module

Fedora

FROM fedora:29

MAINTAINER "Jan Garaj" <info@monitoringartist.com>

# Define required Zabbix version (<version>) or release (release/<version>), e.g. 4.2.2, or release/4.2
ENV ZABBIX_VERSION=release/4.4

WORKDIR /root

RUN \
   dnf -y -q install git automake autoconf gcc make pcre-devel 1>/dev/null && \
   git clone -q https://github.com/monitoringartist/zabbix-docker-monitoring

RUN \
   git clone -b ${ZABBIX_VERSION} --depth 1 https://github.com/zabbix/zabbix.git ~/zabbix && \
   cd ~/zabbix/ && \
   ./bootstrap.sh 1>/dev/null && \
   ./configure --enable-agent 1>/dev/null && \
   cp -R ~/zabbix-docker-monitoring/src/modules/zabbix_module_docker/ ~/zabbix/src/modules/ && \
   cd ~/zabbix/src/modules/zabbix_module_docker && \
   make
