---
description: 未完待续
---

# 初始套装





## 前置准备

```bash
#创建数据保存目录
mkdir -p ${NFS}/initset/conf
mkdir -p ${NFS}/initset/data
mkdir /tmp/tempo
chmod 777 /tmp/tempo

#下载配置文件
wget -O ${NFS}/initset/conf/tempo-local.yaml https://raw.githubusercontent.com/grafana/tempo/main/example/docker-compose/local/tempo-local.yaml
```

## docker-compose.yaml

```yaml
version: "3"
services:

  tempo:
    image: grafana/tempo:latest
    container_name: "tempo"
    command: [ "-config.file=/etc/tempo.yaml" ]
    volumes:
      - ${NFS}/initset/conf/tempo-local.yaml:/etc/tempo.yaml
      - /tmp/tempo:/tmp/tempo
    ports:
      - "14268"  # jaeger ingest
      - "3100"   # tempo
      - "55680"  # otlp grpc
      - "55681"  # otlp http
      - "9411"   # zipkin

  synthetic-load-generator:
    image: omnition/synthetic-load-generator:1.0.25
    volumes:
      - ${NFS}/initset/conf/load-generator.json:/etc/load-generator.json
    environment:
      - TOPOLOGY_FILE=/etc/load-generator.json
      - JAEGER_COLLECTOR_URL=http://tempo:14268
    depends_on:
      - tempo

  prometheus:
    image: prom/prometheus:latest
    container_name: "prometheus"
    command: [ "--config.file=/etc/prometheus.yaml" ]
    volumes:
      - ${NFS}/initset/conf/prometheus.yaml:/etc/prometheus.yaml
    ports:
      - "9090:9090"

  grafana:
    image: grafana/grafana:latest
    container_name: "grafana"
    volumes:
      - ${NFS}/initset/conf/grafana-datasources.yaml:/etc/grafana/provisioning/datasources/datasources.yaml
      - ${NFS}/grafana:/var/lib/grafana
    environment:
      - GF_AUTH_ANONYMOUS_ENABLED=true
      - GF_AUTH_ANONYMOUS_ORG_ROLE=Admin
      - GF_AUTH_DISABLE_LOGIN_FORM=true
      #- GF_SECURITY_ADMIN_PASSWORD=P@ssw0rd123
    labels:
      - "traefik.enable=true"
      - "traefik.docker.network=staging"
      - "traefik.http.services.grafana.loadbalancer.server.port=3000"
      - "traefik.http.routers.grafana.rule=Host(\`grafana.${DOMAIN}\`)"
      - "traefik.http.routers.grafana.entrypoints=http"
      - "traefik.http.routers.grafana-sec.tls=true"
      - "traefik.http.routers.grafana-sec.tls.certresolver=dnsResolver"
      - "traefik.http.routers.grafana-sec.rule=Host(\`grafana.${DOMAIN}\`)"
      - "traefik.http.routers.grafana-sec.entrypoints=https"
    ports:
      - "3000:3000"
      
  traefik:
    image: traefik
    container_name: "traefik"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - ${NFS}/traefik,target=/etc/traefik 
      - ${NFS}/traefik/config:/etc/traefik/config:ro
    command:
      #- "--log.level=DEBUG"
      - "--api.insecure=true"
      - "--providers.docker=true"
      - "--providers.docker.exposedbydefault=false"
      - "--entrypoints.http.address=:80"
      - "--entrypoints.https.address=:443"
      - "--entrypoints.ssh.address=:8022"
      - "--serversTransport.insecureSkipVerify=true"
      - "--api.dashboard=true"
      - "--api.insecure=true"
      - "--providers.docker"
      - "--providers.docker.endpoint=unix:///var/run/docker.sock"
      - "--providers.docker.watch=true"
	    #- "--providers.docker.exposedByDefault=false"
	    - "--providers.docker.useBindPortIP=false"
	    - "--providers.docker.swarmMode=true"
	    - "--providers.docker.network=staging"
    ports:
      - "80:80"
      - "443:443"
      - "8080:8080"
      - "8022:8022"
```

