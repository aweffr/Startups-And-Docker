# Apisix-Dashboard

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 9000 | 管理页面 |



## 命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
-v ${NFS}/apisix/dashboard.yaml:/usr/local/apisix-dashboard/conf/conf.yaml 
-p 9000:9000 
apache/apisix-dashboard:2.3
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name apisix-dashboard \
--network staging \
-e TZ=Asia/Shanghai \
--mount type=bind,src=${NFS}/apisix/dashboard.yaml,dst=/usr/local/apisix-dashboard/conf/conf.yaml \
-p 9000:9000 \
apache/apisix-dashboard:2.3
```
{% endtab %}
{% endtabs %}



## 参考

