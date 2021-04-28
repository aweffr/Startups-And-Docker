# Ocserv

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 8989 | 通讯端口 |



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
--restart unless-stopped \
-e TZ=Asia/Shanghai \
-e VPN_DOMAIN=vpn.easypi.pro \
-e LAN_NETWORK=192.168.0.0 \
-e LAN_NETMASK=255.255.0.0 \
-e VPN_USERNAME=username \
-e VPN_PASSWORD=password \
-p 443:443/tcp \
-p 443:443/udp \
-v ~/ocserv/group.conf:/etc/ocserv/defaults/group.conf \
-v ~/ocserv/client.p12:/etc/ocserv/certs/client.p12 \
-v ~/ocserv/server-cert.pem:/etc/ocserv/certs/server-cert.pem \
vimagick/ocserv
```
{% endtab %}
{% endtabs %}



## 参考

