---
description: 日志聚合系统
---

# Grafana/Loki

## 简介

在Grafana中添加Loki数据源，然后在Explore中查看收集到的日志信息

Loki支持以下应用作为日志数据发送方

官方支持:

* [Promtail](https://grafana.com/docs/loki/latest/clients/promtail/)
* [Docker Driver](https://grafana.com/docs/loki/latest/clients/docker-driver/)
* [Fluentd](https://grafana.com/docs/loki/latest/clients/fluentd/)
* [Fluent Bit](https://grafana.com/docs/loki/latest/clients/fluentbit/)
* [Logstash](https://grafana.com/docs/loki/latest/clients/logstash/)
* [Lambda Promtail](https://grafana.com/docs/loki/latest/clients/lambda-promtail/)

第三方支持:

* [promtail-client](https://github.com/afiskon/promtail-client) \(Go\)
* [push-to-loki.py](https://github.com/sleleko/devops-kb/blob/master/python/push-to-loki.py) \(Python 3\)
* [Serilog-Sinks-Loki](https://github.com/JosephWoodward/Serilog-Sinks-Loki) \(C\#\)
* [loki-logback-appender](https://github.com/loki4j/loki-logback-appender) \(Java\)
* [Log4j2 appender for Loki](https://github.com/tkowalcz/tjahzi) \(Java\)
* [LokiLogger.jl](https://github.com/fredrikekre/LokiLogger.jl) \(Julia\)



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 3100 | 数据接收端口 |



## 前置准备

```bash
#创建数据保存目录
mkdir ${NFS}/grafana

#下载配置文件
wget -O ${NFS}/loki/local-config.yaml https://raw.githubusercontent.com/grafana/loki/main/cmd/loki/loki-docker-config.yaml
```

## 启动命令

{% tabs %}
{% tab title="Docker" %}

{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name loki \
--network staging \
-e TZ=Asia/Shanghai \
--mount type=bind,src=${NFS}/loki,dst=/etc/loki \
--mount type=bind,source=${NFS}/loki/local-config.yaml,target=/etc/loki/local-config.yaml
--label traefik.enable=false \
grafana/loki
```
{% endtab %}
{% endtabs %}



## 参考

官网文档:[https://grafana.com/docs/loki/latest/](https://grafana.com/docs/loki/latest/)  
Github: [https://github.com/grafana/loki](https://github.com/grafana/loki)  
DockerHub: [https://hub.docker.com/r/grafana/loki/](https://hub.docker.com/r/grafana/loki/)

