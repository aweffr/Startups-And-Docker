---
description: 开源云原生网关
---

# Traefik

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 8080 | 管理页面 |
| 80 | HTTP |
| 443 | HTTPS |



## 启动命令

{% tabs %}
{% tab title="Docker" %}


```bash
docker run -d \
--name traefik \
--restart unless-stopped \
-e TZ=Asia/Shanghai \
--privileged \
-p 8080:8080 -p 82:80 -p 444:443 \
-v ${NFS}/traefik/traefik.toml:/etc/traefik/traefik.toml \
-v ${NFS}/traefik/acme:/etc/traefik/acme \
-v /var/run/docker.sock:/var/run/docker.sock \
traefik
```
{% endtab %}

{% tab title="Swarm" %}


```bash
docker service create --replicas 1 \
--name traefik \
--network staging \
-p 8080:8080 \
-p 80:80 -p 444:443 \
--constraint=node.role==manager \
--secret ali_access \
--secret ali_secret \
-e ALICLOUD_ACCESS_KEY_FILE=/run/secrets/ali_access \
-e ALICLOUD_SECRET_KEY_FILE=/run/secrets/ali_secret \
-e TZ=Asia/Shanghai \
--mount type=bind,source=/var/run/docker.sock,target=/var/run/docker.sock \
--mount type=bind,source=${NFS}/traefik,target=/etc/traefik \
traefik
```
{% endtab %}
{% endtabs %}

## 匹配规则

```text
Path: /sub/             匹配请求的子目录
PathPrefix: /sub/*       匹配请求的子目录及包含该子目录的请求
```

## 参考

官 网:[https://traefik.io](https://traefik.io/)

DockerHub:[https://hub.docker.com/\_/traefik](https://hub.docker.com/_/traefik)

中文文档:[https://www.geek-book.com/src/docs/traefik/traefik/docs.traefik.io/index.html](https://www.geek-book.com/src/docs/traefik/traefik/docs.traefik.io/index.html)

