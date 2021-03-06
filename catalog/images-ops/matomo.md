# Matomo

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 80 | 管理页面 |



## 前置准备

```bash
#创建数据保存目录
mkdir ${NFS}/matomo
```

## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name matomo \
--restart unless-stopped \
-e TZ=Asia/Shanghai \
-p 80:80 \
-e MATOMO_DATABASE_ADAPTER=mysql \
-e MATOMO_DATABASE_HOST=mysql \
-e MATOMO_DATABASE_DBNAME=matomo \
-e MATOMO_DATABASE_USERNAME=root \
-e MATOMO_DATABASE_PASSWORD=r00t \
-v ${NFS}/matomo:/var/www/html \
matomo
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name matomo \
--network staging \
-e TZ=Asia/Shanghai \
-e MATOMO_DATABASE_ADAPTER=mysql \
-e MATOMO_DATABASE_HOST=mysql \
-e MATOMO_DATABASE_DBNAME=matomo \
-e MATOMO_DATABASE_USERNAME=root \
-e MATOMO_DATABASE_PASSWORD=r00t \
--mount type=bind,src=${NFS}/matomo,dst=/var/www/html \
matomo

#traefik参数
--label traefik.enable=true \
--label traefik.docker.network=staging \
--label traefik.http.services.matomo.loadbalancer.server.port=80 \
--label traefik.http.routers.matomo.rule="Host(\`matomo.${DOMAIN}\`)" \
--label traefik.http.routers.matomo.entrypoints=http \
--label traefik.http.routers.matomo-sec.tls=true \
--label traefik.http.routers.matomo-sec.tls.certresolver=dnsResolver \
--label traefik.http.routers.matomo-sec.rule="Host(\`matomo.${DOMAIN}\`)" \
--label traefik.http.routers.matomo-sec.entrypoints=https \
```
{% endtab %}
{% endtabs %}

> !注意:不要使用fpm-alpine版本，因为没自带WebServer,而且有坑!

## 参考

