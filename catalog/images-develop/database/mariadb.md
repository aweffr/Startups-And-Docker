# MariaDB

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 3306 | 通讯接口 |



## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name mariadb \
--restart unless-stopped \
--network=backend \
-e ALLOW_EMPTY_PASSWORD=yes \
-v ${NFS}/mariadb:/bitnami/mariadb \
bitnami/mariadb:latest
```
{% endtab %}

{% tab title="Swarm" %}

{% endtab %}
{% endtabs %}



##  参考

官网: [https://mariadb.org/](https://mariadb.org/)

DockerHub: [https://hub.docker.com/\_/mariadb](https://hub.docker.com/_/mariadb)

