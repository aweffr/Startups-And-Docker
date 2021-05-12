---
description: 身份和访问管理解决方案
---

# Keycloak

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 8080 | 管理页面 |



## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d\
--restart unless-stopped \
--network=backend \
--name keycloak \
-h jumpserver \
-p 8080:8080 \
-e KEYCLOAK_USER=admin \
-e KEYCLOAK_PASSWORD=admin \
jboss/keycloak
```
{% endtab %}

{% tab title="Swarm" %}
    docker service create --replicas 1 \
    --network staging \
    -e TZ=Asia/Shanghai \
    --name keycloak \
    -e KEYCLOAK_USER=admin \
    -e KEYCLOAK_PASSWORD=admin \
    jboss/keycloak

    #traefik参数
    --label traefik.enable=true \
    --label traefik.docker.network=staging \
    --label traefik.http.routers.keycloak.rule="Host(\`keycloak.${DOMAIN}\`)" \
    --label traefik.http.routers.keycloak.entrypoints=http \
    --label traefik.http.services.keycloak.loadbalancer.server.port=8080 \
{% endtab %}
{% endtabs %}



## 参考

