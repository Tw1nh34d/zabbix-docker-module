# zabbix-docker-module

docker build --rm=true -t local/zabbix-docker-module-compilation .

docker run --rm -v /tmp:/tmp local/zabbix-docker-module-compilation cp /root/zabbix/src/modules/zabbix_module_docker/zabbix_module_docker.so /tmp/zabbix_module_docker.so

docker rmi -f local/zabbix-docker-module-compilation
