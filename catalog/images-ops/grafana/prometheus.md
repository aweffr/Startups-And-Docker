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

rule_files:
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
        - /etc/prometheus/*.yaml   #指定目标文件的位置(注意文件的权限问题)
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

