---
description: 代码审核(Code Review)
---

# Phabricator

## 简介



## EXPOSE

| 端口 | 用途 |
| :--- | :--- |
| 8080 | HTTP管理入口 |
| 8443 | HTTPS管理入口 |



## 前置准备

```bash
#创建数据保存目录
mkdir ${NFS}/phabricator

```

## 启动命令

{% tabs %}
{% tab title="Docker" %}
```bash
docker run -d --name phabricator \
--restart unless-stopped \
--network=backend \
-p 8080:8080 -p 8443:8443 \
-e ALLOW_EMPTY_PASSWORD=yes \
-e PHABRICATOR_DATABASE_HOST=maria \
-v ${NFS}/phabricator:/bitnami/phabricator \
bitnami/phabricator:latest
```
{% endtab %}

{% tab title="Swarm" %}

{% endtab %}

{% tab title="Compose" %}
```bash
curl -sSL https://raw.githubusercontent.com/bitnami/bitnami-docker-phabricator/master/docker-compose.yml > docker-compose.yml
$ docker-compose up -d
```
{% endtab %}
{% endtabs %}

## 附加参数

**User and Site configuration**

> * `APACHE_HTTP_PORT_NUMBER`: Port used by Apache for HTTP. Default: **8080**
> * `APACHE_HTTPS_PORT_NUMBER`: Port used by Apache for HTTPS. Default: **8443**
> * `PHABRICATOR_USERNAME`: Phabricator application username. Default: **user**
> * `PHABRICATOR_PASSWORD`: Phabricator application password. Default: **bitnami1**
> * `PHABRICATOR_EMAIL`: Phabricator application email. Default: [**user@example.com**](mailto:user@example.com)
> * `PHABRICATOR_FIRSTNAME`: Phabricator user first name. Default: **FirstName**
> * `PHABRICATOR_LASTNAME`: Phabricator user last name. Default: **LastName**
> * `PHABRICATOR_HOST`: Hostname used by Phabricator to form URLs. Default: **127.0.0.1**
> * `PHABRICATOR_ALTERNATE_FILE_DOMAIN`: Alternate domain to use to upload files. No defaults.
> * `PHABRICATOR_USE_LFS`: Whether to configure Phabricator to use GIT Large File Storage \(LFS\). Default: **no**
> * `PHABRICATOR_ENABLE_GIT_SSH_REPOSITORY`: Whether to configure a self-hosted GIT repository with SSH authentication. Default: **no**
> * `PHABRICATOR_SSH_PORT_NUMBER`: Port for SSH daemon. Default: **22**
> * `PHABRICATOR_ENABLE_PYGMENTS`: Whether to enable syntax highlighting using Pygments. Default: **yes**
> * `PHABRICATOR_SKIP_BOOTSTRAP`: Whether to skip the initial bootstrapping for the application \(useful to reuse already populated databases\). Default: **no**

**Use an existing database**

> * `PHABRICATOR_DATABASE_HOST`: Hostname for MariaDB server. Default: **mariadb**
> * `PHABRICATOR_DATABASE_PORT_NUMBER`: Port used by MariaDB server. Default: **3306**
> * `PHABRICATOR_DATABASE_ADMIN_USER`: Database admin user that Phabricator will use to connect with the database server and create its required databases. Default: **root**
> * `PHABRICATOR_DATABASE_ADMIN_PASSWORD`: Database admin password that Phabricator will use to connect with the database server and create its required databases. No defaults.
> * `PHABRICATOR_EXISTING_DATABASE_USER`: Existing user with privileges to modify Phabricator databases when using an already populated database server \(ignored unless `PHABRICATOR_SKIP_BOOTSTRAP=yes`\). No defaults.
> * `PHABRICATOR_DATABASE_ADMIN_PASSWORD`: Password for the existing user mentioned above \(ignored unless `PHABRICATOR_SKIP_BOOTSTRAP=yes`\). No defaults.
> * `ALLOW_EMPTY_PASSWORD`: It can be used to allow blank passwords. Default: **no**

**SMTP Configuration**

> To configure Phabricator to send email using SMTP you can set the following environment variables:
>
> * `PHABRICATOR_SMTP_HOST`: SMTP host.
> * `PHABRICATOR_SMTP_PORT`: SMTP port.
> * `PHABRICATOR_SMTP_USER`: SMTP account user.
> * `PHABRICATOR_SMTP_PASSWORD`: SMTP account password.
> * `PHABRICATOR_SMTP_PROTOCOL`: SMTP protocol. No defaults.

**PHP configuration**

> * `PHP_MAX_EXECUTION_TIME`: Maximum execution time for PHP scripts. No default.
> * `PHP_MAX_INPUT_TIME`: Maximum input time for PHP scripts. No default.
> * `PHP_MAX_INPUT_VARS`: Maximum amount of input variables for PHP scripts. No default.
> * `PHP_MEMORY_LIMIT`: Memory limit for PHP scripts. Default: **256M**
> * `PHP_POST_MAX_SIZE`: Maximum size for PHP POST requests. No default.
> * `PHP_UPLOAD_MAX_FILESIZE`: Maximum file size for PHP uploads. No default.
> * `PHP_ENABLE_OPCACHE`: Enable OPcache for PHP scripts. No default.
> * `PHP_EXPOSE_PHP`: Enables HTTP header with PHP version. No default.

## 参考

官网: [https://www.phacility.com/](https://www.phacility.com/)  
官方文档: [https://secure.phabricator.com/book/phabricator/](https://secure.phabricator.com/book/phabricator/)

