# zabbix-docker-module

<h1>Dockerfiles</h1>
taken from
<br>https://github.com/monitoringartist/zabbix-docker-monitoring

<h1>Patch</h1> 
taken from (thx <a href="https://github.com/tambetliiv">@tambetliiv</a>)
<br>https://github.com/monitoringartist/zabbix-docker-monitoring/issues/133#issuecomment-558535199
<br>
docker build --rm=true -t local/zabbix-docker-module-compilation .

docker run --rm -v /tmp:/tmp local/zabbix-docker-module-compilation cp /root/zabbix/src/modules/zabbix_module_docker/zabbix_module_docker.so /tmp/zabbix_module_docker.so

docker rmi -f local/zabbix-docker-module-compilation
