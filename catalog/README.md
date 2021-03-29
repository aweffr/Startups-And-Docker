# 应用目录

### 基础应用

| 名称 | 用途 | 内存占用 | 备注 |
| :---: | :---: | :---: | :---: |
| [Traefik](images-base/traefik.md) | 网关 | 25M | 替代Nginx转发功能 |
| [APISix](images-base/apisix/) | API网关 |  | - |
| [Nginx](images-base/nginx.md) | Web Server | 3M | - |
| [NextCloud](images-base/nexcloud.md) | OAuth供应器,WebDAV,文件共享 | 126M | 可将文件存储至Minio |
| [Minio](images-base/minio.md) | 对象存储 | 165M | 兼容S3协议 |
| [Ocserv](images-base/ocserv.md) | OpenConnect VPN服务端 |  | 兼容Cisco Anyconnect |
| [Bitwarden](images-base/bitwarden.md) | 开源的密码管理服务 |  | 供客户端程序使用 |

### 开发应用

| 名称 | 用途 | 内存占用 | 备注 |
| :---: | :---: | :---: | :---: |
| [MariaDB](images-develop/shu-ju-ku/mariadb.md) | MySQL替代品 |  | - |
| [MySQL](images-develop/shu-ju-ku/mysql/) | 数据库 | 180M | - |
| [Postgres](images-develop/shu-ju-ku/postgres/) | 数据库 | 7M | - |
| [MongoDB](images-develop/shu-ju-ku/mongodb/) | 数据库 | 1000M | - |
| [Redis](images-develop/huan-cun/redis.md) | 键值对\(Key-Value\)存储数据库 | 4.5M | - |
| [Etcd](images-base/etcd.md) | Key/Value 存储系统 | 75M | 用于分享配置和服务发现 |
| [Adminer](images-develop/shu-ju-ku/adminer.md) | 多类型数据库管理 |  | 类似PhpMyAdmin |
| [YApi](images-develop/yapi.md) | 接口管理文档 |  | - |
| [Flyway](images-develop/flyway.md) | 数据库脚本管理 |  | - |

### CI/CD

| 名称 | 用途 | 内存占用 | 备注 |
| :---: | :---: | :---: | :---: |
| [Gitea](images-cicd/gitea.md) | 版本控制 | 250M | Gogs分叉版本，支持OAuth2 |
| [Drone](images-cicd/drone/) | 自动编译发布 | 21M | 适合发布服务端程序 |
| [Jekins](images-cicd/jekins.md) | 自动编译发布 | 1.051G | 适合发布客户端程序 |

### 运维环境

| 名称 | 用途 | 内存占用 | 备注 |
| :---: | :---: | :---: | :---: |
| [Portainer](images-ops/portainer.md) | 网页版Docker管理 | 16M | - |
| [Matomo](images-ops/matomo.md) |  |  | - |
| Elkarbackup | 数据备份 |  | - |
| Alerta | 报警信息整合 |  | - |
| [Dnsmasq](images-ops/dnsmasq.md) | DNS解析 | 9.45M | - |
| [Grafana](images-ops/grafana/) | 数据可视化工具 |  | - |
| [Grafana/Loki](images-ops/grafana/grafana-loki.md) | 日志聚合系统 | 需配置grafana使用 | - |

