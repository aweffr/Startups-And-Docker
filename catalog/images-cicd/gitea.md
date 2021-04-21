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
-e DOMAIN="gitea.${DOMAIN}" \
-e SSH_DOMAIN="gitea.${DOMAIN}" \
-e SSH_PORT=8022 \
gitea/gitea

#traefik参数
--label traefik.enable=true \
--label traefik.docker.network=staging \
--label traefik.http.routers.gitea.rule="Host(\`gitea.${DOMAIN}\`)" \
--label traefik.http.routers.gitea.entrypoints=http \
--label traefik.http.services.gitea.loadbalancer.server.port=3000 \
```
{% endtab %}
{% endtabs %}

> 如从内网其它主机导入版本库不允许从私有IP导入，可通过在${NFS}/gitea/gitea/conf/app.ini中添加以下参数并重启解决

```text
[migrations]
ALLOW_LOCALNETWORKS = true
```

##  参考

官网:  [https://gitea.io/zh-cn/](https://gitea.io/zh-cn/)

配置说明: [https://docs.gitea.io/zh-cn/config-cheat-sheet/](https://docs.gitea.io/zh-cn/config-cheat-sheet/)

