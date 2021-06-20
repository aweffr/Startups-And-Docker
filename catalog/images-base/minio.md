---
description: 兼容S3的对象存储服务
---

# Minio

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 9000 | 管理页面+API接口 |



## 前置准备

```bash
#创建数据保存目录
mkdir -p ${NFS}/minio/data
mkdir -p ${NFS}/minio/conf
```

## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d \
--name minio \
--restart unless-stopped \
--network=backend \
-e TZ=Asia/Shanghai \
-v ${NFS}/minio/data:/data \
-v ${NFS}/minio/conf:/root/.minio \
-p 9000:9000 \
minio/minio server /data
```
{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name minio \
--network staging \
-e TZ=Asia/Shanghai \
-e "MINIO_REGION_NAME=Area1" \
-e "MINIO_BROWSER=on" \
-e "MINIO_ROOT_USER=minioadmin" \
-e "MINIO_ROOT_PASSWORD=wJalrXUtnFEMI/K7MD8NG/bPxRfiBY7XAMPLEKEY" \
--mount type=bind,src=${NFS}/minio/data,dst=/data \
--mount type=bind,src=${NFS}/minio/conf,dst=/root/.minio \
minio/minio server /data

#traefik参数
--label traefik.enable=true \
--label traefik.docker.network=staging \
--label traefik.http.services.minio.loadbalancer.server.port=9000 \
--label traefik.http.routers.minio.rule="Host(\`minio.${DOMAIN}\`)" \
--label traefik.http.routers.minio.entrypoints=http \
--label traefik.http.routers.minio-sec.tls=true \
--label traefik.http.routers.minio-sec.tls.certresolver=dnsResolver \
--label traefik.http.routers.minio-sec.rule="Host(\`minio.${DOMAIN}\`)" \
--label traefik.http.routers.minio-sec.entrypoints=https \
```
{% endtab %}
{% endtabs %}



## 参考

官网: [https://min.io/](https://min.io/)

DockerHub: [https://hub.docker.com/r/minio/minio](https://hub.docker.com/r/minio/minio)

参考手册: [https://docs.min.io/cn/minio-quickstart-guide.html](https://docs.min.io/cn/minio-quickstart-guide.html)

