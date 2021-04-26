# Redis

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 6379 | 通讯端口 |
| 8080 | 管理页面 |



## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name redis \
--net backend \
-e TZ=Asia/Shanghai \
--restart unless-stopped \
-v ${NFS}/redis:/data \
-p 6379:6379 \
redis:alpine --requirepass Ttt123456 --appendonly yes
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name redis \
--network staging \
-e TZ=Asia/Shanghai \
-p 6379:6379 \
redis:alpine --requirepass Ttt123456
```
{% endtab %}
{% endtabs %}



##  参考

