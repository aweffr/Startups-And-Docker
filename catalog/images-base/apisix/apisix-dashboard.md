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
--network=backend \
--restart unless-stopped \
-e TZ=Asia/Shanghai \
--name apisix-dashboard
-v ${NFS}/apisix/dashboard.yaml:/usr/local/apisix-dashboard/conf/conf.yaml 
-p 9000:9000 
apache/apisix-dashboard:2.6
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name apisix-dashboard \
--network staging \
-e TZ=Asia/Shanghai \
--mount type=bind,src=${NFS}/apisix/dashboard.yaml,dst=/usr/local/apisix-dashboard/conf/conf.yaml \
apache/apisix-dashboard:2.6

#traefik参数
--label traefik.enable=true \
--label traefik.docker.network=staging \
--label traefik.http.routers.apisix.rule="Host(\`apisix.${DOMAIN}\`)" \
--label traefik.http.routers.apisix.entrypoints=http \
--label traefik.http.services.apisix.loadbalancer.server.port=9000 \
```
{% endtab %}
{% endtabs %}

> Dashboard版本号与相应的Apisix版本的并不同步，目前高0.1

## 参考

