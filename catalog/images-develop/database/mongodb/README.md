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
--secret MONGO_PWD \
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
--secret MONGO_PWD \
-e MONGO_INITDB_ROOT_USERNAME="mongoadmin" \
-e MONGO_INITDB_ROOT_PASSWORD_FILE=/run/secrets/MONGO_PWD \
--label traefik.enable=false \
mongo
```
{% endtab %}
{% endtabs %}



开启用户验证\(MongoDB默认任何人都可修改数据库\)

```bash
docker exec -it 容器ID /bin/bash
db.auth('mongoadmin','r00t')

添加用户(可选)
db.createUser({user:"用户名",pwd:"密码",roles:[{role: 'root', db: 'admin'}]})

```

##  参考

