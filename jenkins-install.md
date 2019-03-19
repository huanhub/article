---
title: jenkins 安装
date: 2018-01-29 21:40:36
tags:
  - '工具'
---

Jenkins 是基于Java开发的一种持续集成工具，用于监控持续重复的工作，旨在提供一个开放易用的软件平台，使开发者从繁杂的集成中解脱出来，专注于更为重要的业务逻辑实现上。

<!-- more -->

## 本文的安装环境

* Centos 7 以上
* JDK 1.8
* nginx 1.12.0

###  安装 JDK 1.8

* 下载官方rpm 包 [点击进入](http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html)
* rpm包安装
```bash
# rpm -ivh jdk-8u162-linux-x64.rpm
# javac -version
javac 1.8.0_162
# java -version
java version "1.8.0_162"
Java(TM) SE Runtime Environment (build 1.8.0_162-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.162-b12, mixed mode)
```

### 安装Jenkins

```bash
# curl http://pkg.jenkins-ci.org/redhat/jenkins.repo -o /etc/yum.repos.d/jenkins.repo
# rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
# yum -y install jenkins
```

> 默认安装的相关目录
jenkins home目录  /var/lib/jenkins
jenkins 配置文件目录  /etc/sysconfig/jenkins
其中默认端口是 8080, 如果需要修改其他端口，需要在配置文件里面修改


### 设置开机启动并启动服务

```bash
# systemctl enable jenkins
# service jenkins start
```

### 配置nginx

```bash
# jenkins is upstream listening on port 8080
upstream jenkins {
        server                          127.0.0.1:8080 fail_timeout=0;
}

# nginx is listening on port 80
server {
  listen                          80;
  server_name                     jenkins.example.com;

  location / {

      proxy_set_header        Host $host:$server_port;
      proxy_set_header        X-Real-IP $remote_addr;
      proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header        X-Forwarded-Proto $scheme;

      proxy_pass              http://jenkins;
  }
}

```

配置完重启nginx后，就可以访问Jenkins服务进行初始化管理员和密码进行配置了


### 其他相关

* 为jenkins 用户生成ssh私钥和公钥
```bash
# sudo -u jenkins ssh-keygen
```
