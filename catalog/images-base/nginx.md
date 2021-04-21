---
description: Web Server
---

# Nginx

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 80 | HTTP |
| 443 | HTTPS |



## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name nginx \
--restart unless-stopped \
--net backend \
-e TZ=Asia/Shanghai \
-p 80:80 \
-p 443:443 \
-v ${NFS}/nginx/data/www:/var/web \
-v ${NFS}/nginx/conf/nginx.conf:/etc/nginx/nginx.conf:ro \
-v ${NFS}/nginx/conf/vhost:/etc/nginx/vhost:ro \
nginx:stable-alpine
```
{% endtab %}

{% tab title="Swarm" %}
```bash
#使用host模式映射端口会失去负载均衡功能，但可以取到真实IP
docker service create --replicas 1 \
--name nginx \
--network staging \
--publish mode=host,target=80,published=80 \
--publish mode=host,target=443,published=443 \
-e TZ=Asia/Shanghai \
--mount type=bind,src=${NFS}/nginx/data/www,dst=/var/web \
--mount type=bind,src=${NFS}/nginx/conf/nginx.conf,dst=/etc/nginx/nginx.conf,readonly \
--mount type=bind,src=${NFS}/nginx/conf/vhost,dst=/etc/nginx/vhost,readonly \
nginx:stable-alpine

#traefik参数(同时需去除--publish参数)
--label traefik.enable=true \
--label traefik.docker.network=staging \
--label traefik.http.routers.nginx.rule="Host(\`www.${DOMAIN}\`)" \
--label traefik.http.routers.nginx.entrypoints=http \
--label traefik.http.services.nginx.loadbalancer.server.port=80 \
```
{% endtab %}
{% endtabs %}



## 参考

