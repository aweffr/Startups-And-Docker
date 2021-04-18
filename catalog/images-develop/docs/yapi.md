# YApi

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 4001 | 管理页面 |



## 启动命令

{% tabs %}
{% tab title="Docker" %}

{% endtab %}

{% tab title="Swarm" %}
```
docker service create --replicas 1 \
--name yapi \
--network staging \
-e YAPI_CLOSE_REGISTER=false \
-e YAPI_DB_SERVERNAME=mongo \
-e YAPI_DB_USER=root \
-e YAPI_DB_PASS=r00t \
-e YAPI_PLUGINS=[{"name":"oauth2","options":{}}, \
{"name":"interface-oauth2-token","options":{}}, \
{"name":"notifier","options":{}}, \
{"name":"pl-test-dashboard","options":{}}] \
{"name":"response-to-ts","options":{}}, \
{"name":"proxy-jkdh","options":{}}, \
jayfong/yapi

```
{% endtab %}
{% endtabs %}



##  参考

Docker说明 [https://github.com/fjc0k/docker-YApi](https://github.com/fjc0k/docker-YApi)

