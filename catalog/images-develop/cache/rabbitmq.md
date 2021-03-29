---
description: 开源消息队列
---

# RabbitMQ

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 5672 | 通讯端口 |
| 15672 | 管理页面 |



## 命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name rabbitmq \
--net backend \
--restart unless-stopped \
-e RABBITMQ_VM_MEMORY_HIGH_WATERMARK="1024MiB" \
-e RABBITMQ_DEFAULT_USER="guest" \
-e RABBITMQ_DEFAULT_PASS="guest" \
-v ${NFS}/rabbitmq:/var/lib/rabbitmq \
-p 5672:5672 \
-p 15672:15672 \
rabbitmq:management-alpine
```
{% endtab %}

{% tab title="Swarm" %}

{% endtab %}
{% endtabs %}



## 参考

