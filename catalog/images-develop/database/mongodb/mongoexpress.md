# MongoExpress

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 8081 | 管理页面 |



## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -it --rm \
--name mongo-express \
--restart unless-stopped \
--network backend \
-p 8081:8081 \
-e ME_CONFIG_OPTIONS_EDITORTHEME="ambiance" \
-e ME_CONFIG_MONGODB_SERVER="mongo" \
-e ME_CONFIG_BASICAUTH_USERNAME="mongoadmin" \
-e ME_CONFIG_BASICAUTH_PASSWORD="r00t" \
mongo-express
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--network staging \
-e TZ=Asia/Shanghai \
--name mongo-express \
--restart unless-stopped \
--network backend \
-e ME_CONFIG_OPTIONS_EDITORTHEME="ambiance" \
-e ME_CONFIG_MONGODB_SERVER="mongo" \
-e ME_CONFIG_BASICAUTH_USERNAME="mongoadmin" \
-e ME_CONFIG_BASICAUTH_PASSWORD="r00t" \
mongo-express
```
{% endtab %}
{% endtabs %}



##  参考

