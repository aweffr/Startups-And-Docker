# MemCached

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 11211 | 通讯端口 |



## 启动命令

{% tabs %}
{% tab title="Docker" %}
```text
docker run -d \
--name memcached \
--net backend \
--restart unless-stopped \
--net backend \
-p 11211:11211 \
memcached:alpine
```
{% endtab %}

{% tab title="Swarm" %}

{% endtab %}
{% endtabs %}



## 参考

