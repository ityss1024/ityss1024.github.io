---
layout: article
title: zabbix-server安装脚本
mathjax: true
---


```shell
## docker安装
#!/bin/bash
docker run --name mysql-server -t -e TZ=Asia/Shanghai -e MYSQL_DATABASE="zabbix" -e MYSQL_USER="zabbix" -e MYSQL_PASSWORD="zabbix@dxc.com" -e MYSQL_ROOT_PASSWORD="zabbix@dxc.com" -d mysql:5.7 --character-set-server=utf8 --collation-server=utf8_bin

docker run --name zabbix-java-gateway -e TZ=Asia/Shanghai -t -d zabbix/zabbix-java-gateway:latest

docker run --name zabbix-server-mysql -t -e TZ=Asia/Shanghai -e DB_SERVER_HOST="mysql-server" -e MYSQL_DATABASE="zabbix" -e MYSQL_USER="zabbix" -e MMSQL_PASSWORD="zabbix@dxc.com" -e MYSQL_ROOT_PASSWORD="zabbix@dxc.com" -e ZBX_JAVAGATEWAY="zabbix-java-gateway" --link mysql-server:mysql --link zabbix-java-gateway:zabbix-java-gateway -p 10051:10051 -d zabbix/zabbix-server-mysql:latest

docker run --name zabbix-web-nginx-mysql -t -e TZ=Asia/Shanghai -e DB_SERVER_HOST="mysql-server" -e MYSQL_DATABASE="zabbix" -e MYSQL_USER="zabbix" -e MMSQL_PASSWORD="zabbix@dxc.com" -e MYSQL_ROOT_PASSWORD="zabbix@dxc.com" --link mysql-server:mysql --link zabbix-server-mysql:zabbix-server -p 9080:8080 -d zabbix/zabbix-web-nginx-mysql:latest

docker run --name zabbix-agent -e TZ=Asia/Shanghai -e ZBX_HOSTNAME="Zabbix server" -e ZBX_SERVER_HOST="zabbix-server-mysql" --link zabbix-server-mysql:zabbix-server -d zabbix/zabbix-agent:latest

```


