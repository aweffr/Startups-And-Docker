# Grafana/Loki

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 53 | DNS |
| 8080 | 管理页面 |



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

