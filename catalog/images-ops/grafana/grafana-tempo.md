---
description: 分布式跟踪后端
---

# Grafana/Tempo

## 简介

与 Grafana，Prometheus 和 Loki 深度集成分布式跟踪后端，可以使用 Jaeger，Zipkin，OpenCensus 和 OpenTelemetry 中的任何一个追踪协议。

Tempo配置相对比较复杂，你可以通过\[[官方范例](https://github.com/grafana/tempo/tree/main/example/docker-compose)\]获得所有配置文件参数及docker-compose文件。

## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 55680 | OpenTelemetry |
| 6831 | Jaeger - Thrift Compact |
| 6832 | Jaeger - Thrift Binary |
| 14268 | Jaeger - Thrift HTTP |
| 14250 | Jaeger - GRPC |
| 9411 | Zipkin |



## 前置准备

```bash
#创建数据保存目录
mkdir ${NFS}/tempo
mkdir /tmp/tempo
chmod 777 /tmp/tempo

#下载配置文件
wget -O ${NFS}/tempo/tempo-local.yaml https://raw.githubusercontent.com/grafana/tempo/main/example/docker-compose/local/tempo-local.yaml
```

## 启动命令

{% tabs %}
{% tab title="Docker" %}

{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name tempo \
--network staging \
-e TZ=Asia/Shanghai \
--mount type=bind,src=${NFS}/tempo/tempo-local.yaml,dst=/etc/tempo.yaml \
--mount type=bind,src=/tmp/tempo,dst=/tmp/tempo \
grafana/tempo \
--config.file='/etc/tempo.yaml'
```
{% endtab %}
{% endtabs %}



## 参考

官网: [https://grafana.com/oss/tempo/](https://grafana.com/oss/tempo/)  
官方文档: [https://grafana.com/docs/tempo/latest/](https://grafana.com/docs/tempo/latest/)  
Github: [https://github.com/grafana/tempo](https://github.com/grafana/tempo)

