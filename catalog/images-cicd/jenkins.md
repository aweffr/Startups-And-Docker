---
description: 开源持续集成工具
---

# Jenkins

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 8080 | 管理页面 |
| 50000 |  |



## 命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name jenkins \
--restart unless-stopped \
--network=backend \
-e TZ=Asia/Shanghai \
-p 8080:8080 \
-p 50000:50000 \
-v ${NFS}/jenkins:/var/jenkins_home \
jenkins/jenkins:alpine
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name jenkins \
--network staging \
-e TZ=Asia/Shanghai \
-p 8080:8080 \
-p 50000:50000 \
--mount type=bind,src=${NFS}/jenkins,dst=/var/jenkins_home \
jenkins/jenkins:alpine
```
{% endtab %}
{% endtabs %}



##  参考

官网: [https://www.jenkins.io/](https://www.jenkins.io/)

