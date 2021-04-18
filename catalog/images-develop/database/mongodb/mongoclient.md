# MongoClient

## 简介

内存占用约110M\(使用内置mongodb\)、64M\(使用外部mongodb\)

本配置使用外部mongodb存储mongo-client数据+web登录时需验证

## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 3000 | 管理页面 |



## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name mongo-client \
--restart unless-stopped \
--net backend \
-e MONGO_URL="mongodb://mongoadmin:r00t@mongo:27017" \
-e MONGOCLIENT_AUTH=true \
-e MONGOCLIENT_USERNAME="webadmin" \
-e MONGOCLIENT_PASSWORD="webr00t" \
-p 3000:3000 \
mongoclient/mongoclient
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name mongo-client \
--network staging \
-e TZ=Asia/Shanghai \
--restart unless-stopped \
--net backend \
-e MONGO_URL="mongodb://mongoadmin:r00t@mongo:27017" \
-e MONGOCLIENT_AUTH=true \
-e MONGOCLIENT_USERNAME="webadmin" \
-e MONGOCLIENT_PASSWORD="webr00t" \
mongoclient/mongoclient
```
{% endtab %}
{% endtabs %}



##  参考

