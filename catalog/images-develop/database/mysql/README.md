# MySQL

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 3306 | 通讯端口 |



## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name mysql \
--restart unless-stopped \
--net backend \
-p 3306:3306 \
-e TZ=Asia/Shanghai \
-e MYSQL_ROOT_PASSWORD=Test123456 \
-v ${NFS}/mysql:/var/lib/mysql \
mysql --lower_case_table_names=1
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name mysql \
--network staging \
-p 3306:3306 \
-e TZ=Asia/Shanghai \
-e MYSQL_ROOT_PASSWORD=Test123456 \
--mount type=bind,src=${NFS}/mysql,dst=/var/lib/mysql \
mysql --lower_case_table_names=1
```
{% endtab %}
{% endtabs %}

> lower\_case\_table\_names参数可忽略表名大小写，Windows平台程序员常用

##  参考

