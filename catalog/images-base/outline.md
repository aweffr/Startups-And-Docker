---
description: Gitbook开源替代品
---

# Outline

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 53 | DNS |
| 8080 | 管理页面 |



## 前置准备

```bash
#创建数据保存目录
mkdir ${NFS}/doku
```

## 启动命令

{% tabs %}
{% tab title="Docker" %}

{% endtab %}

{% tab title="Swarm" %}

{% endtab %}

{% tab title="Compose" %}
{% code title="outline.yml" %}
```yaml
version: "3"
services:
    outline:
    image: outlinewiki/outline
    container_name: outline
    networks: staging
    command: sh -c "yarn sequelize:migrate --env production-ssl-disabled && yarn start"
    environment:
      - DATABASE_URL: postgres://user:pass@postgres:5432/outline
      - DATABASE_URL_TEST: postgres://user:pass@postgres:5432/outline-test
      - REDIS_URL: redis://redis:6379
      - FORCE_HTTPS: false
      - DEFAULT_LANGUAGE: zh_CN
      #- TEAM_LOGO: https://example.com/images/logo.png
      - SECRET_KEY: generate_a_new_key
      - UTILS_SECRET: generate_a_new_key
    env_file:
      - ./env.outline
      - ./env.slack
    restart: always
    depends_on:
      - postgres
      - redis
      - minio
```
{% endcode %}
{% endtab %}
{% endtabs %}



## 参考

