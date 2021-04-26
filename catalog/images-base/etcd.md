---
description: 管理配置信息和服务发现
---

# Etcd

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 2379 |  |
| 2380 |  |



## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name etcd-server \
-v /mnt/nfs/etcd/etcd.conf.yml:/opt/bitnami/etcd/conf/etcd.conf.yml \
-p 2379:2379 \
-p 2380:2380  \
-e TZ=Asia/Shanghai \
-e ETCD_ENABLE_V2=true \
--env ALLOW_NONE_AUTHENTICATION=yes \
--env ETCD_ADVERTISE_CLIENT_URLS=http://etcd-server:2379 \
bitnami/etcd:latest --enable-v2=true
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name etcd-server \
--network staging \
-e TZ=Asia/Shanghai \
-e ETCD_ENABLE_V2=true \
-e ALLOW_NONE_AUTHENTICATION=yes \
-e ETCD_ADVERTISE_CLIENT_URLS=http://0.0.0.0:2379 \
-e ETCD_LISTEN_CLIENT_URLS=http://0.0.0.0:2379 \
--label traefik.enable=false \
bitnami/etcd:latest
```
{% endtab %}
{% endtabs %}



## 参考

