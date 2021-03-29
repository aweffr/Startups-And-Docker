# Secret

## 说明

从Docker 1.13开始在集群状态下可以使用Secret来保存敏感数据\(密码，证书，文件\)



## 用法

```text
#密码
printf "zabbix" | docker secret create MYSQL_PASSWORD -
##或
echo 'zabbix' | docker secret create MYSQL_PASSWORD -
##用法
-e MYSQL_PASSWORD_FILE=/run/secrets/MYSQL_PASSWORD
##或
--secret my-pass

#查看密码列表
docker secret ls
```

## 

## 参考

[https://docs.docker.com/engine/swarm/secrets/](https://docs.docker.com/engine/swarm/secrets/)

