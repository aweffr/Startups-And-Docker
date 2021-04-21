# 应用目录

### 基础应用

| 名称 | 用途 | 内存占用 | 备注 |
| :---: | :---: | :---: | :---: |
| [Traefik](images-base/traefik.md) | 网关 | 25M | 替代Nginx转发功能 |
| [APISix](images-base/apisix/) | API网关 |  | - |
| [Nginx](images-base/nginx.md) | Web Server | 3M | - |
| [NextCloud](images-base/nexcloud.md) | OAuth供应器,WebDAV,文件共享 | 126M | 可将文件存储至Minio |
| [Minio](images-base/minio.md) | 对象存储 | 165M | 兼容S3协议 |
| [Wordpress](images-base/wordpress.md) | 开源博客平台 |  | - |
| [Synapse](images-base/synapse.md) | 聊天室服务器 | 87M |  |
| [Dokuwiki](images-base/dokuwiki.md) | Wiki |  | - |
| [Ocserv](images-base/ocserv.md) | OpenConnect VPN服务端 |  | 兼容Cisco Anyconnect |
| [Bitwarden](images-base/bitwarden.md) | 开源的密码管理服务 |  | 供客户端程序使用 |

### 开发应用

| 名称 | 用途 | 内存占用 | 备注 |
| :---: | :---: | :---: | :---: |
| [MariaDB](images-develop/database/mariadb.md) | MySQL替代品 |  | - |
| [MySQL](images-develop/database/mysql/) | 数据库 | 180M | - |
| [Postgres](images-develop/database/postgres/) | 数据库 | 7M | - |
| [MongoDB](images-develop/database/mongodb/) | 数据库 | 166M | - |
| [Redis](images-develop/cache/redis.md) | 键值对\(Key-Value\)存储数据库 | 4.5M | - |
| [RabbitMQ](images-develop/cache/rabbitmq.md) | 开源消息队列 | 83M |  |
| [Etcd](images-base/etcd.md) | Key/Value 存储系统 | 75M | 用于分享配置和服务发现 |
| [Adminer](images-develop/database/adminer.md) | 多类型数据库管理 |  | 类似PhpMyAdmin |
| [YApi](images-develop/docs/yapi.md) | 接口管理文档 |  | - |
| [Flyway](images-develop/docs/flyway.md) | 数据库脚本管理 |  | - |

### CI/CD

| 名称 | 用途 | 内存占用 | 备注 |
| :---: | :---: | :---: | :---: |
| [Gitea](images-cicd/gitea.md) | 版本控制 | 115M | Gogs分叉版本，支持OAuth2和S3 |
| [Phabricator](images-cicd/phabricator.md) | 代码审核 |  | 界面比Gerrit更人性化 |
| [Drone](images-cicd/drone/) | 开源持续集成工具 | 21M | 适合发布服务端程序 |
| [Jenkins](images-cicd/jenkins.md) | 开源持续集成工具 | 1.051G | 适合发布客户端程序 |

### 运维环境

| 名称 | 用途 | 内存占用 | 备注 |
| :---: | :---: | :---: | :---: |
| [Portainer](images-ops/portainer.md) | 网页版Docker管理 | 16M | - |
| [Matomo](images-ops/matomo.md) |  |  | - |
| Elkarbackup | 数据备份 |  | - |
| Alerta | 报警信息整合 |  | - |
| [Dnsmasq](images-ops/dnsmasq.md) | DNS解析 | 9.45M | - |
| Zabbix | 企业级开源监控方案 | 37M | - |
| [Grafana](images-ops/grafana/) | 数据可视化工具 | 13M | - |
| [Grafana/Loki](images-ops/grafana/grafana-loki.md) | 日志聚合系统 |  | 需配合Grafana使用 |
| [Prometheus](images-ops/grafana/prometheus.md) | 服务监控 |  | 也是时序数据库 |

