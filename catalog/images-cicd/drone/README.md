# Drone

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 80 | HTTP管理入口 |
| 443 | HTTPS管理入口 |



## 前置准备

```bash
#创建数据保存目录
mkdir ${NFS}/drone
```

## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name drone \
--restart unless-stopped \
--network=backend \
-e DRONE_AGENTS_ENABLED=true \
-e DRONE_USER_CREATE=rakutens \
-e DRONE_SERVER_HOST=drone.${DOMAIN} \
-e DRONE_SERVER_PROTO=http \
-e DRONE_LOGS_TRACE=true \
-e DRONE_LOGS_DEBUG=true \
-e DRONE_GOGS_SERVER=http://gogs:3000 \
-e DRONE_RPC_SECRET=MWckgvhjqg4E3eQ0ptg2X4iNC6oQiyU4LLvO4eXFFuHtrTkIy2vwcAc3erB5f9reM \
-p 80:80 \
-p 443:443 \
drone/drone
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name drone \
--network staging \
-e TZ=Asia/Shanghai \
-e DRONE_AGENTS_ENABLED=true \
-e DRONE_USER_CREATE=username:rakutens,admin:true \
-e DRONE_SERVER_HOST=drone.${DOMAIN} \
-e DRONE_SERVER_PROTO=http \
-e DRONE_LOGS_DEBUG=true \
-e DRONE_GIT_ALWAYS_AUTH=true \
-e DRONE_GIT_USERNAME=drone \
-e DRONE_GIT_PASSWORD=Drone!23 \
-e DRONE_GOGS_SERVER=http://gogs:3000 \
-e DRONE_WEBHOOK_ENDPOINT=http://drone/hook \
-e DRONE_RPC_SECRET=MWckgvhjqg4E3eQ0ptg2X4iNC6oQiyU4LLvO4eXFFuHtrTkIy2vwcAc3erB5f9reM \
--mount type=bind,src=${NFS}/drone,dst=/data \
--mount type=bind,source=/var/run/docker.sock,target=/var/run/docker.sock \
drone/drone

#traefik参数
--label traefik.enable=true \
--label traefik.docker.network=staging \
--label traefik.http.routers.drone.rule="Host(\`drone.${DOMAIN}\`)" \
--label traefik.http.routers.drone.entrypoints=http \
--label traefik.http.services.drone.loadbalancer.server.port=80 \
```
{% endtab %}
{% endtabs %}



##  参考

