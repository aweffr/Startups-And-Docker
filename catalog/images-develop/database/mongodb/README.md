# MongoDB

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 27017 | 通讯端口 |

## 前置准备

```bash
#创建数据保存目录
mkdir ${NFS}/mongo

#将密码保存进Docker Secret
echo 'r00t' | docker secret create MONGO_PWD -
```

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
-e MONGO_INITDB_ROOT_PASSWORD_FILE=/run/secrets/MONGO_PWD \
-p 27017:27017 \
mongo
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--network staging \
-e TZ=Asia/Shanghai \
--name mongo \
--mount type=bind,src=${NFS}/mongo,dst=/data/db \
-e MONGO_INITDB_ROOT_USERNAME="mongoadmin" \
-e MONGO_INITDB_ROOT_PASSWORD_FILE=/run/secrets/MONGO_PWD \
--label traefik.enable=false \
mongo
```
{% endtab %}
{% endtabs %}



##  参考

