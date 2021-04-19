---
description: 开源Wiki应用
---

# Dokuwiki

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
```
{% endtab %}
{% endtabs %}



## 参考

官网: [https://www.dokuwiki.org/](https://www.dokuwiki.org/dokuwiki)

