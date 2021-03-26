# Swarm

#### 创建overlay网桥

`(默认的overlay不带自动发现无法通过名称调用到其它容器)`

docker network create -d overlay staging

#### 滚动升级

docker service update --image nginx:stable-alpine nginx

#### 扩展实例数量

docker service scale nginx=2

#### 退出当前Swarm

docker swarm leave --force

#### 密码

```text
printf "zabbix" | docker secret create MYSQL_PASSWORD -
#或
echo 'zabbix' | docker secret create MYSQL_PASSWORD -

用法
-e MYSQL_PASSWORD_FILE=/run/secrets/MYSQL_PASSWORD
或
--secret my-pass
```

#### 查看密码列表

docker secret ls

