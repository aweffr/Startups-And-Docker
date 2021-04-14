---
description: phpMyAdmin的替代品
---

# Adminer

## 简介

支持多种数据库的管理工具\(MySQL，SQLite，PostgreSQL，MS SQL，Oracle\)

## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 8080 | 管理页面 |



## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--network=backend \
--name adminer \
--restart unless-stopped \
-e TZ=Asia/Shanghai \
-p 8081:8080 \
-e ADMINER_DESIGN='nette' \
adminer
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name adminer \
--network staging \
-e TZ=Asia/Shanghai \
-p 8081:8080 \
-e TZ=Asia/Shanghai \
-e ADMINER_DESIGN='nette' \
adminer
```
{% endtab %}
{% endtabs %}



##  参考

官网: [https://www.adminer.org/](https://www.adminer.org/)

