---
description: DNS服务器端
---

# Dnsmasq

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 53 | DNS |
| 8080 | 管理页面 |



## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name dnsmasq \
--restart unless-stopped \
--network backend \
-e TZ=Asia/Shanghai \
-p 53:53/udp \
-p 8080:8080 \
-v ${NFS}/dnsmasq/dnsmasq.conf:/etc/dnsmasq.conf \
--log-opt "max-size=100m" \
-e "HTTP_USER=admin" \
-e "HTTP_PASS=test123" \
jpillora/dnsmasq
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name dnsmasq \
--network staging \
-p 53:53/udp \
-e TZ=Asia/Shanghai \
--mount type=bind,src=${NFS}/dnsmasq/dnsmasq.conf,dst=/etc/dnsmasq.conf \
--log-opt "max-size=100m" \
-e "HTTP_USER=admin" \
-e "HTTP_PASS=test123" \
jpillora/dnsmasq
```
{% endtab %}
{% endtabs %}



## 参考

