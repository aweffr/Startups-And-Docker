# Postgres

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 5432 | 通讯端口 |



## 前置准备

```bash
#创建数据保存目录
mkdir ${NFS}/postgrea

#将密码保存进Docker Secret
echo 'Test123666' | docker secret create POSTGRES_PWD -
```

## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name postgres \
--restart unless-stopped \
--net backend \
--shm-size=256MB \
-e TZ=Asia/Shanghai \
--secret POSTGRES_PWD \
-e POSTGRES_USER=admin \
-e POSTGRES_PASSWORD_FILE=/run/secrets/POSTGRES_PWD \
-p 5432:5432 \ 
-v ${NFS}/postgres:/var/lib/postgresql/data \
postgres:alpine
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name postgres \
--network staging \
-e TZ=Asia/Shanghai \
--secret POSTGRES_PWD \
-e POSTGRES_USER=admin \
-e POSTGRES_PASSWORD_FILE=/run/secrets/POSTGRES_PWD \
--mount type=tmpfs,dst=/dev/shm,tmpfs-size=268435456 \
--mount type=bind,src=${NFS}/postgres,dst=/var/lib/postgresql/data \
--label traefik.enable=false \
postgres:alpine
```
{% endtab %}

{% tab title="Compose" %}
```
version: "3"
networks:
  staging
  
services:
  postgres:
    image: postgres
    container_name: postgres
    secrets:
      - POSTGRES_PWD
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD_FILE: /run/secrets/POSTGRES_PWD
    tmpfs: /dev/shm,tmpfs-size=268435456
    volumes: 
      - ${NFS}/postgres:/var/lib/postgresql/data
    labels:
      - traefik.enable: false
    logging:
      driver: loki
      options: 
        -loki-url: "http://loki:3100/api/prom/push
    restart: unless-stopped
secrets:
  POSTGRES_PWD:
    external: true
```
{% endtab %}
{% endtabs %}

> Alpine版镜像更小，但不支持GIS

##  参考

