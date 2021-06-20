---
description: 日志采集系统
---

# Promtail

## 简介

收集硬盘上log文件内容并发送给Loki实例



## 前置准备

```bash
#创建数据保存目录
mkdir ${NFS}/promtail

```

## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash

```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name promtail \
--network staging \
-e TZ=Asia/Shanghai \
--mount type=bind,src=${NFS}/promtail,dst=/etc/promtail \
--mount type=bind,src=/var/log,dst=/var/log \
--label traefik.enable=false \
grafana/promtail
```
{% endtab %}
{% endtabs %}



## 参考

