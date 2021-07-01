---
description: 服务监控
---

# Prometheus

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 9090 | 通讯端口 |



## 前置准备

```bash
#创建数据保存目录
mkdir -p ${NFS}/prometheus/conf
mkdir ${NFS}/prometheus/data
chmod 777 ${NFS}/prometheus/data
touch ${NFS}/prometheus/conf/targets.json

#创建配置文件
vi ${NFS}/prometheus/conf/prometheus.yml
```

* prometheus.yml

```yaml
global:
  scrape_interval:     15s
  evaluation_interval: 15s
  
# Alertmanager configuration
alerting:
  alertmanagers:
  - static_configs:
    - targets:
      # - alertmanager:9093

#rule_files:
  # - "alert.rules"
  # - "first.rules"
  # - "second.rules"

scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: 'prometheus'
    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.
    static_configs:
    - targets: ['localhost:9090']
    
  - job_name: 'file_ds'
     file_sd_configs:       #以 file_sd_configs 动态发现的模式，推荐使用这种方式，可以实现热添加
     - refresh_interval: 1m    #指定多久扫描一次目标配置文件
       files:
        - /etc/prometheus/targets.yaml   #指定目标文件的位置(注意文件的权限问题)
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
-v ${NFS}/prometheus/conf:/etc/prometheus \
-v ${NFS}/prometheus/data:/prometheus/data \
prom/prometheus
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name prometheus \
--network staging \
-e TZ=Asia/Shanghai \
-p 9090:9090 \
--mount type=bind,src=${NFS}/prometheus/conf,dst=/etc/prometheus \
--mount type=bind,src=${NFS}/prometheus/data,dst=/prometheus \
--label traefik.enable=false \
prom/prometheus
```
{% endtab %}
{% endtabs %}

## Node Exporter

{% tabs %}
{% tab title="Linux" %}
* 运行exporter容器

```bash
docker run -d \
-p 9100:9100 \
--name node-exporter \
--net=backend \
--restart always \
-v /proc:/host/proc \
-v /sys:/host/sys \
-v /:/rootfs \
prom/node-exporter \
--path.procfs=/host/proc \
--path.sysfs=/host/sys \
--collector.filesystem.ignored-mount-points="^/(sys|proc|dev|host|etc)($|/)"
```

* targets.json中添加内容

```javascript
{
    "targets": [
      "node ip:9100"
    ],
    "labels": {
      "job": "Linux"
    }
}
```

* Grafana添加面板: 左边栏 + 号 &gt; Import &gt; 输入 10467 &gt; 点击Load按钮
{% endtab %}

{% tab title="Windows" %}
* 下载软件 [https://github.com/prometheus-community/windows\_exporter/releases/latest](https://github.com/prometheus-community/windows_exporter/releases/latest) \(如:windows\_exporter-0.16.0-amd64.msi\)
* 双击运行
* 打开Windows入站防火墙端口9182
* targets.json中添加内容

```javascript
{
    "targets": [
      "服务器ip:9182"
    ],
    "labels": {
      "job": "windows"
    }
}
```

* Grafana添加面板: 左边栏 + 号 &gt; Import &gt; 输入 10467 &gt; 点击Load按钮
{% endtab %}

{% tab title="Docker" %}
* 运行cAdvisor容器

```bash
#使用ucloud加速的google官方镜像

docker run -d \
--name=cadvisor \
--restart always \
--privileged \
-v /:/rootfs:ro \
-v /var/run:/var/run:ro \
-v /sys:/sys:ro \
-v /var/lib/docker/:/var/lib/docker:ro \
-v /dev/disk/:/dev/disk:ro \
-p 18081:8080 \
uhub.service.ucloud.cn/gcr_io/cadvisor:latest
```

* targets.json中添加内容

```javascript
{
    "targets": [
      "服务器ip:18081"
    ],
    "labels": {
      "job": "docker"
    }
}
```

* Grafana添加面板: 左边栏 + 号 &gt; Import &gt; 输入 14282 &gt; 点击Load按钮
{% endtab %}
{% endtabs %}



## 参考

