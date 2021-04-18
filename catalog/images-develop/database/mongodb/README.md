# MongoDB

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 27017 | 通讯端口 |



## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name mongo \
--restart unless-stopped \
--net backend \
-v ${NFS}/mongo:/data/db \
-e MONGO_INITDB_ROOT_USERNAME="mongoadmin" \
-e MONGO_INITDB_ROOT_PASSWORD="r00t" \
-p 27017:27017 \
mongo
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name mongo \
--network staging \
-e TZ=Asia/Shanghai \
-v ${NFS}/mongo:/data/db \
-e MONGO_INITDB_ROOT_USERNAME="mongoadmin" \
-e MONGO_INITDB_ROOT_PASSWORD="r00t" \
mongo
```
{% endtab %}
{% endtabs %}



##  参考

