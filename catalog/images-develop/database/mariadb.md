# MariaDB

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 3306 | 通讯接口 |



## 前置准备

```bash
#创建数据保存目录
mkdir ${NFS}/maria

#将密码保存进Docker Secret
echo 'Test123456' | docker secret create MARIA_PWD -
```

## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name maria \
--restart unless-stopped \
--network=backend \
-p 3306:3306 \
-e ALLOW_EMPTY_PASSWORD=yes \
-v ${NFS}/maria:/bitnami/mariadb \
bitnami/mariadb:latest
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name maria \
--network staging \
-p 3306:3306 \
-e TZ=Asia/Shanghai \
--mount type=bind,src=${NFS}/maria,dst=/bitnami/mariadb \
--label traefik.enable=false \
bitnami/mariadb:latest
```
{% endtab %}
{% endtabs %}



##  参考

官网: [https://mariadb.org/](https://mariadb.org/)

DockerHub: [https://hub.docker.com/\_/mariadb](https://hub.docker.com/_/mariadb)

