---
description: 跳板机
---

# JumpServer

## 简介

默认帐号：admin 密码：admin

## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 80 | 管理页面 |
| 2222 | 通讯接口 |



## 前置准备

1. [部署MySQL](../images-develop/database/mysql/)
2. [部署Redis](../images-develop/cache/redis.md)
3. 生成随机加密密钥

```bash
if [ "$SECRET_KEY" = "" ]; then SECRET_KEY=`cat /dev/urandom | tr -dc A-Za-z0-9 | head -c 50`; echo "SECRET_KEY=$SECRET_KEY" >> ~/.bashrc; echo $SECRET_KEY; else echo $SECRET_KEY; fi

if [ "$BOOTSTRAP_TOKEN" = "" ]; then BOOTSTRAP_TOKEN=`cat /dev/urandom | tr -dc A-Za-z0-9 | head -c 16`; echo "BOOTSTRAP_TOKEN=$BOOTSTRAP_TOKEN" >> ~/.bashrc; echo $BOOTSTRAP_TOKEN; else echo $BOOTSTRAP_TOKEN; fi
```

4. 初始化数据库

```bash
# docker exec -it mysql /bin/bash
# mysql -u root -p abcd@1234
mysql> create database jumpserver default charset 'utf8mb4';
mysql> grant all on jumpserver.* to 'jumpserver'@'%' identified by 'abcd@1234';
mysql> flush privileges;
mysql> exit;
# exit
```

5. 创建数据目录

```bash
#创建数据保存目录
mkdir ${NFS}/jumpserver
```

## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--restart unless-stopped \
--network=backend \
--name jumpserver \
-h jumpserver \
-p 80:80 \
-p 2222:2222 \
-e SECRET_KEY=$SECRET_KEY \
-e BOOTSTRAP_TOKEN=$BOOTSTRAP_TOKEN \
-e DB_HOST=mysql \
-e DB_USER=jumpserver \
-e DB_PASSWORD="abcd@1234" \
-e DB_NAME=jumpserver \
-e REDIS_HOST=redis \
-e REDIS_PASSWORD="123456" \
-v ${NFS}/jumpserver:/opt/jumpserver/data/media \
jumpserver/jms_all
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--network staging \
-e TZ=Asia/Shanghai \
--name jumpserver \
-h jumpserver \
-e SECRET_KEY=$SECRET_KEY \
-e BOOTSTRAP_TOKEN=$BOOTSTRAP_TOKEN \
-e DB_HOST=mysql \
-e DB_USER=jumpserver \
-e DB_PASSWORD="abcd@1234" \
-e DB_NAME=jumpserver \
-e REDIS_HOST=redis \
-e REDIS_PASSWORD="123456" \
--mount type=bind,src=${NFS}/jumpserver,dst=/opt/jumpserver/data/media \
jumpserver/jms_all

--label traefik.enable=true \
--label traefik.docker.network=staging \
--label traefik.http.routers.jumpserver.rule="Host(\`jumpserver.${DOMAIN}\`)" \
--label traefik.http.routers.jumpserver.entrypoints=http \
--label traefik.http.services.jumpserver.loadbalancer.server.port=80 \
```
{% endtab %}
{% endtabs %}



## 参考

官网 [http://www.jumpserver.org](http://www.jumpserver.org)   
文档 [http://docs.jumpserver.org](http://docs.jumpserver.org)

