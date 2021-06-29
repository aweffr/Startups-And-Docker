---
description: synapse网页版客户端
---

# element-web

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 80 | WEB入口 |



## 前置准备

```bash
#创建数据保存目录
mkdir ${NFS}/element

wget -O ${NFS}/element/config.json https://raw.githubusercontent.com/vector-im/element-web/develop/element.io/app/config.json
```

## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name element \
--net backend \
-p 80:80\
-e TZ=Asia/Shanghai \
-v ${NFS}/element-web/config.json:/app/config.json \
vectorim/element-web
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name element \
--network staging \
-e TZ=Asia/Shanghai \
-e LANG=C.UTF-8 \
-e LC_ALL=C.UTF-8 \
--mount type=bind,src=${NFS}/element-web/config.json,dst=/app/config.json \
--label traefik.enable=true \
--label traefik.docker.network=staging \
--label traefik.http.services.chat.loadbalancer.server.port=80 \
--label traefik.http.routers.chat.rule="Host(\`chat.${DOMAIN}\`)" \
--label traefik.http.routers.chat.entrypoints=http \
--label traefik.http.routers.chat-sec.tls=true \
--label traefik.http.routers.chat-sec.tls.certresolver=dnsResolver \
--label traefik.http.routers.chat-sec.rule="Host(\`chat.${DOMAIN}\`)" \
--label traefik.http.routers.chat-sec.entrypoints=https \
vectorim/element-web
```
{% endtab %}
{% endtabs %}



## 参考

