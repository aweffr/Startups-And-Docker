# PhpMyAdmin

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 80 | 管理页面 |



## 命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name myadmin \
--restart unless-stopped \
--net backend \
-e TZ=Asia/Shanghai \
-e PMA_ARBITRARY=1 \
-p 8081:80 \
phpmyadmin/phpmyadmin
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name myadmin \
--network staging \
-e TZ=Asia/Shanghai \
-e PMA_ARBITRARY=1 \
-e PMA_HOST=mysql \
-p 8081:80 \
phpmyadmin/phpmyadmin
```
{% endtab %}
{% endtabs %}

> PMA\_ARBITRARY 可连接其它数据库 
>
> PMA\_HOST 默认数据库地址,相同network情况下可直接使用MySQL容器的name参数值

##  参考

