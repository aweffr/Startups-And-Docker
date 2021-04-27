# PgAdmin4

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 80 | 管理页面 |



## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
-e PGADMIN_DEFAULT_EMAIL=user@domain.com \
-e PGADMIN_DEFAULT_PASSWORD=SuperSecret \
-p 8082:80 \
dpage/pgadmin4
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name pgadmin \
--network staging \
-e TZ=Asia/Shanghai \
-e PGADMIN_DEFAULT_EMAIL=admin@domain.com \
-e PGADMIN_DEFAULT_PASSWORD=SuperSecret \
-p 8082:80 \
dpage/pgadmin4
```
{% endtab %}
{% endtabs %}



##  参考

PgAdmin4帮助: [链接](https://www.pgadmin.org/docs/pgadmin4/latest/container_deployment.html)

