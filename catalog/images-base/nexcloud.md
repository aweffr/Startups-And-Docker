# NexCloud

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 80 | 管理页面 |



## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name nextcloud \
--restart unless-stopped \
-e TZ=Asia/Shanghai \
-v ${NFS}/nextcloud:/var/www/html \
-p 8080:80 \
nextcloud
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name nextcloud \
--network staging \
-e TZ=Asia/Shanghai \
--label traefik.enable=true \
--label traefik.docker.network=staging \
--label traefik.http.routers.cloud.rule="Host(\`cloud.${DOMAIN}\`)" \
--label traefik.http.routers.cloud.entrypoints=http \
--label traefik.http.services.cloud.loadbalancer.server.port=80 \
--mount type=bind,src=${NFS}/nextcloud,dst=/var/www/html \
nextcloud

#traefik参数
--label traefik.enable=true \
--label traefik.docker.network=staging \
--label traefik.http.routers.cloud.rule="Host(\`cloud.${DOMAIN}\`)" \
--label traefik.http.routers.cloud.entrypoints=http \
--label traefik.http.services.cloud.loadbalancer.server.port=80 \
```
{% endtab %}
{% endtabs %}



## 参考

OAuth2说明: [https://docs.nextcloud.com/server/20/admin\_manual/configuration\_server/oauth2.html](https://docs.nextcloud.com/server/20/admin_manual/configuration_server/oauth2.html)

