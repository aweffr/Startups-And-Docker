# YApi

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 3000 | 管理页面 |



## 启动命令

{% tabs %}
{% tab title="Docker" %}

{% endtab %}

{% tab title="Swarm" %}
    docker service create --replicas 1 \
    --name yapi \
    --network staging \
    -e YAPI_CLOSE_REGISTER=false \
    -e YAPI_DB_SERVERNAME=mongo \
    -e YAPI_DB_USER=root \
    -e YAPI_DB_PASS=r00t \
    -e YAPI_PLUGINS="[{\"name\":\"oauth2\",\"options\":{}}, \
    {\"name\":\"interface-oauth2-token\",\"options\":{}}, \
    {\"name\":\"notifier\",\"options\":{}}, \
    {\"name\":\"pl-test-dashboard\",\"options\":{}}, \
    {\"name\":\"response-to-ts\",\"options\":{}}, \
    {\"name\":\"proxy-jkdh\",\"options\":{}}]" \
    jayfong/yapi


    #traefik参数
    --label traefik.enable=true \
    --label traefik.docker.network=staging \
    --label traefik.http.routers.yapi.rule="Host(\`yapi.${DOMAIN}\`)" \
    --label traefik.http.routers.yapi.entrypoints=http \
    --label traefik.http.services.yapi.loadbalancer.server.port=3000 \
{% endtab %}
{% endtabs %}



##  参考

Docker说明 [https://github.com/fjc0k/docker-YApi](https://github.com/fjc0k/docker-YApi)

