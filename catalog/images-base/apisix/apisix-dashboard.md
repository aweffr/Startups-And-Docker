# Apisix-Dashboard

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
-v ${NFS}/apisix/dashboard.yaml:/usr/local/apisix-dashboard/conf/conf.yaml 
-p 9000:9000 
apache/apisix-dashboard:2.3
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name apisix-dashboard \
--network staging \
-e TZ=Asia/Shanghai \
--mount type=bind,src=${NFS}/apisix/dashboard.yaml,dst=/usr/local/apisix-dashboard/conf/conf.yaml \
-p 9000:9000 \
apache/apisix-dashboard:2.3

#traefik参数
--label traefik.enable=true \
--label traefik.docker.network=staging \
--label traefik.http.routers.api.rule="Host(\`api.${DOMAIN}\`)" \
--label traefik.http.routers.api.entrypoints=http \
--label traefik.http.services.api.loadbalancer.server.port=80 \
```
{% endtab %}
{% endtabs %}



## 参考

