---
description: 可视化容器管理工具
---

# Portainer

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 9000 | 管理页面 |



## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name portainer \
--restart unless-stopped \
-e TZ=Asia/Shanghai \
--privileged \
-p 9000:9000 \
-v /var/run/docker.sock:/var/run/docker.sock \
portainer/portainer
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name portainer \
--network staging \
-e TZ=Asia/Shanghai \
--mount type=bind,source=/var/run/docker.sock,target=/var/run/docker.sock \
portainer/portainer:1.24.1-alpine
```
{% endtab %}
{% endtabs %}



## 参考



