---
description: 如果我只有一台4G内存的ECS但却啥都想要怎么办?
---

# 前言

## 源头

本来只是一个用于快速查找docker镜像启动参数的Markdown文件，当内容越积越多后，发现是时候需要重新整理一下了。

## 目标

这份文档的本意是让人们只需要5分钟就把所有环境架起来，而不是浪费一下午去研究某个应用要怎么搞，目标人群是已经有一定Docker基础的技术型人群，不考虑K8S或PodMan，因为它们没办法跑在Windows下，而入门级用户或初创型企业很有可能就只是在用Windows.....

## 原则

所有入选的镜像原则依据为~~\(唯一性&gt;资源占用&gt;普及度\)~~单纯个人喜好，虽然现在大厂对K8S非常推崇，但其资源占用量与复杂度却非常不讨喜，而Docker Swarm在资源占用及学习曲线上对新手及初创性公司却非常友好\(500台宿主机也完全能撑得住\)，如果你非常想用K8S，也可以用podman导出compose.yaml来跑，当然以后我们可能也会直接提供compose.yaml，但什么时候很难讲，请不要太期待。



## 最后

坑先刨了，慢慢填....







**推荐参考**

[https://yeasy.gitbook.io/docker\_practice/](https://yeasy.gitbook.io/docker_practice/)



