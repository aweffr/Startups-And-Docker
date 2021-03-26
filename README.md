# 目录



### 基础环境

| 名称 | 用途 | 内存占用 | 备注 |
| :---: | :---: | :---: | :---: |
| Traefik | 网关 | 25M | 替代Nginx转发功能 |
| APISix | API网关 |  | - |
| Nginx | Web Server | 3M | - |
| NextCloud | OAuth供应器,WebDAV,文件共享 | 126M | 可将文件存储至Minio |
| Minio | 对象存储 | 165M | 兼容S3协议 |
| Ocserv | OpenConnect VPN服务端 |  | 兼容Cisco Anyconnect |
| Bitwarden | 开源的密码管理服务 |  | - |

### 开发环境

| 名称 | 用途 | 内存占用 | 备注 |
| :---: | :---: | :---: | :---: |
| MariaDB | MySQL替代品 |  | - |
| MySQL | 数据库 | 180M | - |
| Postgres | 数据库 | 7M | - |
| MongoDB | 数据库 | 1000M | - |
| Redis | 键值对\(Key-Value\)存储数据库 | 4.5M | - |
| etcd | Key/Value 存储系统 | 75M | 用于分享配置和服务发现 |
| Adminer | 多类型数据库管理 |  | 类似PhpMyAdmin |
| YApi | 接口管理文档 |  | - |
| Flyway | 数据库脚本管理 |  | - |

### CI/CD

| 名称 | 用途 | 内存占用 | 备注 |
| :---: | :---: | :---: | :---: |
| Gitea | 版本控制 | 250M | Gogs分叉版本，支持OAuth2 |
| Drone | 自动编译发布 | 21M | 适合发布服务端程序 |
| Jekins | 自动编译发布 | 1.051G | 适合发布客户端程序 |

### 运维环境

| 名称 | 用途 | 内存占用 | 备注 |
| :---: | :---: | :---: | :---: |
| Portainer | 网页版Docker管理 | 16M | - |
| Elkarbackup | 数据备份 |  | - |
| jpillora/dnsmasq | DNS解析 | 9.45M | - |
| grafana | 数据可视化工具 |  | - |
| grafana/loki | 日志聚合系统 | 需配置grafana使用 | - |

