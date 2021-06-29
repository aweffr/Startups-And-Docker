---
description: synapse网页版客户端
---

# element-web

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 53 | DNS |
| 8080 | 管理页面 |



## 前置准备

```bash
#创建数据保存目录
mkdir ${NFS}/element
```

## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name element \
--net backend \
-p 80:80\
-e TZ=Asia/Shanghai \
-v ${NFS}/element-web/config.json:/app/config.json \
vectorim/element-web
```
{% endtab %}

{% tab title="Swarm" %}

{% endtab %}
{% endtabs %}



## 参考

