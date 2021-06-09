---
description: OpenConnect VPN服务端
---

# Ocserv

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 443/TCP | 通讯端口 |
| 443/UDP | 通讯端口 |



## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name ocserv \
--restart unless-stopped \
--privileged \
-p 8989:8989/tcp \
-v /nfs/data/ocserv:/etc/ocserv \
wppurking/ocserv
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name ocserv \
--network staging \
-e TZ=Asia/Shanghai \
-e VPN_DOMAIN=vpn.easypi.pro \
-e LAN_NETWORK=192.168.0.0 \
-e LAN_NETMASK=255.255.0.0 \
-e VPN_USERNAME=username \
-e VPN_PASSWORD=password \
--mount type=bind,src=${NFS}/ocserv/group.conf,dst=/etc/ocserv/defaults/group.conf \
--mount type=bind,src=${NFS}/ocserv/client.p12,dst=/etc/ocserv/certs/client.p12 \
--mount type=bind,src=${NFS}/ocserv/server-cert.pem,dst=/etc/ocserv/certs/server-cert.pem \
vimagick/ocserv
```
{% endtab %}
{% endtabs %}



## 参考

