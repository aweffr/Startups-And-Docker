---
description: 服务监控
---

# Prometheus

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 53 | DNS |
| 8080 | 管理页面 |



## 前置准备

```bash
#创建数据保存目录
mkdir ${NFS}/prometheus

```

## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
-p 9090:9090 \
--name prometheus \
--net=backend \
--restart always \
-v ${NFS}/prometheus/conf/prometheus.yml:/etc/prometheus/prometheus.yml \
-v ${NFS}/prometheus/data:/prometheus/data \
prom/prometheus \
--config.file=/etc/prometheus/prometheus.yml
```
{% endtab %}

{% tab title="Swarm" %}
```bash

```
{% endtab %}
{% endtabs %}



## 参考

