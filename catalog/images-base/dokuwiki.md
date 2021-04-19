---
description: 开源Wiki应用
---

# Dokuwiki

## 简介

小巧实用并且功能强大的Wiki系统，使用文件系统而不是数据库来保存数据，拥有丰富的[插件库](https://www.dokuwiki.org/plugins)并且支持OAuth2，具体差别可查看[与MediaWiki的区别](https://www.wikimatrix.org/compare/dokuwiki+mediawiki)

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
--name dokuwiki \
--net backend \
-p 80:80 -p 443:443 \
-e TZ=Asia/Shanghai \
-v ${NFS}/dokuwiki:/bitnami \
bitnami/dokuwiki:latest
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name dokuwiki \
--network staging \
-p 80:80 -p 443:443 \
-e TZ=Asia/Shanghai \
--mount type=bind,src=${NFS}/dokuwiki,dst=/bitnami \
bitnami/dokuwiki:latest

#traefik参数
--label traefik.enable=true \
--label traefik.docker.network=staging \
--label traefik.http.routers.wiki.rule="Host(\`wiki.${DOMAIN}\`)" \
--label traefik.http.routers.wiki.entrypoints=http \
--label traefik.http.services.wiki.loadbalancer.server.port=80 \
```
{% endtab %}
{% endtabs %}



## 参考

官网: [https://www.dokuwiki.org/](https://www.dokuwiki.org/dokuwiki)

