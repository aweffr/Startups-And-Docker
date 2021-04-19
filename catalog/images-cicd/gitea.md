# Gitea

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 22 | SSH |
| 3000 | 管理页面 |



## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name gitea \
--restart unless-stopped \
--network=backend \
-v ${NFS}/gitea:/data \
-e DB_TYPE=mysql
-e DB_HOST=db:3306
-e DB_NAME=gitea
-e DB_USER=gitea
-e DB_PASSWD=gitea
-p 3000:3000 \
-p 8022:22 \
gitea/gitea
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name gitea \
--hostname gitea.mytrade.fun \
--network staging \
--mount type=bind,src=${NFS}/gitea,dst=/data \
--mount type=bind,src=/etc/timezone,dst=/etc/timezone:ro \
--mount type=bind,src=/etc/localtime,dst=/etc/localtime:ro \
-e DB_TYPE=mysql \
-e DB_HOST=db:3306 \
-e DB_NAME=gitea \
-e DB_USER=gitea \
-e DB_PASSWD=gitea \
--label traefik.enable=true \
--label traefik.docker.network=staging \
--label traefik.http.routers.gitea.rule="Host(\`gitea.mytrade.fun\`)" \
--label traefik.http.routers.gitea.entrypoints=http,https \
--label traefik.http.routers.gitea.tls.certresolver=certbot \
--label traefik.http.services.gitea.loadbalancer.server.port=3000 \
--label traefik.tcp.routers.gitea.rule="Host(\`gitea.mytrade.fun\`)" \
--label traefik.tcp.routers.gitea.entrypoints=ssh \
--label traefik.tcp.services.gitea.loadbalancer.server.port=22 \
--label traefik.tcp.routers.gitea.tls.certresolver=certbot \
gitea/gitea
```
{% endtab %}
{% endtabs %}



##  参考

官网:  [https://gitea.io/zh-cn/](https://gitea.io/zh-cn/)

