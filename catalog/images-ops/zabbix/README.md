# Zabbix

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 162 |  |
| 10051 |  |



## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name zabbix-server \
--restart unless-stopped \
--network backend \
-p 162:162 -p 10051:10051 \
-e DB_SERVER_HOST="mysql" \
-e MYSQL_USER="root" \
-e MYSQL_PASSWORD="Test123456" \
-v ${NFS}/data/zabbix/alertscripts:/usr/lib/zabbix/alertscripts \
-v ${NFS}/data/zabbix/externalscripts:/usr/lib/zabbix/externalscripts \
-v ${NFS}/data/zabbix/modules:/var/lib/zabbix/modules \
zabbix/zabbix-server-mysql
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name zabbix-server \
--network staging \
-e TZ=Asia/Shanghai \
-e DB_SERVER_HOST="mysql" \
-e MYSQL_USER="root" \
-e MYSQL_PASSWORD="Test123456" \
-e ZBX_UNREACHABLEDELAY=30 \
-p 162:162 -p 10051:10051 \
--mount type=bind,src=${NFS}/zabbix/data/alertscripts,dst=/usr/lib/zabbix/alertscripts \
--mount type=bind,src=${NFS}/zabbix/data/externalscripts,dst=/usr/lib/zabbix/externalscripts \
--mount type=bind,src=${NFS}/zabbix/data/modules,dst=/var/lib/zabbix/modules \
zabbix/zabbix-server-mysql
```
{% endtab %}
{% endtabs %}



## 参考

