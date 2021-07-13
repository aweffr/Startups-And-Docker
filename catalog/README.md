---
description: 数据库脚本管理
---

# 应用目录

### 基础应用

| 名称 | 用途 | 内存占用 |   端口映射 | 备注 |
| :---: | :---: | :---: | :---: | :---: |
| [Traefik](images-base/traefik.md) | 网关 | 25M | 80,443,8080 | 替代Nginx转发功能 |
| [APISix](images-base/apisix/) | API网关 | 103M | 9080,9443 | - |
| [Nginx](images-base/nginx.md) | Web Server | 3M | 80,443 | - |
| [NextCloud](images-base/nexcloud.md) | OAuth供应器,WebDAV,文件共享 | 126M | 80 | 可将文件存储至Minio |
| [Minio](images-base/minio.md) | 对象存储 | 165M | 9000 | 兼容S3协议 |
| [Wordpress](images-base/wordpress.md) | 开源博客平台 |  | 80 | - |
| Flarum | 开源论坛 |  |  |  |
| [Synapse](images-base/synapse/) | 聊天室服务器 | 87M | 8008,8448 |  |
| [Dokuwiki](images-base/dokuwiki.md) | Wiki |  | 80,443 | - |
| [Outline](images-base/outline.md) | Gitbook开源替代品 |  | 3000 |  |
| [Ocserv](images-base/ocserv.md) | OpenConnect VPN服务端 |  | 443 | 兼容Cisco Anyconnect |
| [Bitwarden](images-base/bitwarden.md) | 开源的密码管理服务 |  | 53,8080 | 供客户端程序使用 |
| PhotoPrism | 照片分享平台 |  |  |  |

### 开发应用

| 名称 | 用途 | 内存占用 | 端口映射 | 备注 |
| :---: | :---: | :---: | :---: | :---: |
| [MariaDB](images-develop/database/mariadb.md) | MySQL替代品 |  | 3306 | - |
| [MySQL](images-develop/database/mysql/) | 数据库 | 180M | 3306 | - |
| [Postgres](images-develop/database/postgres/) | 数据库 | 7M | 5432 | - |
| [MongoDB](images-develop/database/mongodb/) | 数据库 | 65M | 27017 |  |
| [MemCached](images-develop/cache/memcached.md) | 键值对\(Key-Value\)存储数据库 |  | 11211 |  |
| [Redis](images-develop/cache/redis.md) | 键值对\(Key-Value\)存储数据库 | 4.5M | 6379 | - |
| [RabbitMQ](images-develop/cache/rabbitmq.md) | 开源消息队列 | 83M | 5672,15672 |  |
| [Adminer](images-develop/database/adminer.md) | 多类型数据库管理 |  | 8080 | 类似PhpMyAdmin |
| [YApi](images-develop/docs/yapi.md) | 接口管理文档 |  | 3000 | - |
| Flyway | 数据库脚本管理 |  |  | - |

### CI/CD

| 名称 | 用途 | 内存占用 | 端口映射 | 备注 |
| :---: | :---: | :---: | :---: | :---: |
| [Gitea](images-cicd/gitea.md) | 版本控制 | 115M | 22,3000 | Gogs分叉版本，支持OAuth2和S3 |
| [Phabricator](images-cicd/phabricator.md) | 代码审核 |  | 8080,8443 | 界面比Gerrit更人性化 |
| [Drone](images-cicd/drone/) | 开源持续集成工具 | 21M | 80,443 | 适合发布服务端程序 |
| [Jenkins](images-cicd/jenkins.md) | 开源持续集成工具 | 1.051G | 8080,50000 | 适合发布客户端程序 |

### 运维环境

| 名称 | 用途 | 内存占用 | 端口映射 | 备注 |
| :---: | :---: | :---: | :---: | :---: |
| [Portainer](images-ops/portainer.md) | 网页版Docker管理 | 16M | 9000 | - |
| [Keycloak](images-ops/keycloak.md) | 身份和访问管理解决方案 |  | 8080 |  |
| [Matomo](images-ops/matomo.md) |  |  | 80 | - |
| Elkarbackup | 数据备份 |  |  | - |
| Alerta | 报警信息整合 |  |  | - |
| [Dnsmasq](images-ops/dnsmasq.md) | DNS解析 | 9.45M | 53,8080 | - |
| [JumpServer](images-ops/jumpserver.md) | 跳板机 | 1220M | 80,2222 |  |
| [Zabbix](images-ops/zabbix/) | 企业级开源监控方案 | 37M | 162,10051 | - |
| [Etcd](images-ops/etcd.md) | Key/Value 存储系统 | 75M | 2379,2380 | 用于分享配置和服务发现 |
| [Grafana](images-ops/grafana/) | 数据可视化工具 | 13M | 3000 | - |
| [Grafana/Loki](images-ops/grafana/grafana-loki/) | 日志聚合系统 | 35M | 3100 | 需配合Grafana使用 |
| [Grafana/Promtail](images-ops/grafana/grafana-loki/grafana-promtail.md) | 日志采集系统 | 20M |  | 需配合Loki使用 |
| [Prometheus](images-ops/grafana/prometheus/) | 服务监控 | 354M | 9090 | 也是时序数据库 |

