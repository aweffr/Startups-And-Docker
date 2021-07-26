# Linux



```bash
#添加新用户
#-d 指定用户home目录
#-s 指定shell(rbash为受限shell,不能切换目录)
sudo useradd -m 用户名 -g 组名 -d /home/用户名 -s /bin/rbash
sudo passwd 密码


#删除帐号
userdel 用户名
```



```bash
## 找到进程的pid
ps -ef|grep 程序名

## 查看该进程的状态
top -p 进程id

## 每隔1秒查看进程状态，总共10次的数据
pidstat 1 10
```

