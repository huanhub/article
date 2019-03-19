---
title: 使用jenkins和phabricator搭建自动发布的博客
date: 2018-01-29 18:09:01
tags:
  - '工具'
---

本文的主要思路是使用Phabricator托管的git服务，通过创建harbormaster构建计划和创建herald通知规则触发Jenkins的构建任务自动部署github page’s 博客

<!-- more -->

### 本文的安装环境

* Centos 7 以上
* nginx 1.12.0
* Jenkins [点击进入安装教程](http://blog.haohuan.org/posts/201801/jenkins-install/)
* Phabricator

### 创建git库

在 Phabricator 上的找到 `Diffusion` -> `Create Repository` 创建一个git库 或使用现有的git库 `repository name`

### 在 Phabricator 创建Bot 用户 jenkins

把 Jenkins 系统用户的 公钥放到 Phabricator 的jenkins 用户上

### 在Jenkins 创建一个自由风格的项目

在 源码管理 里选择 Git 设置 刚创建完成的 git 库地址，添加 git库的认证

在 构建触发器 里勾选 触发远程构建 (例如,使用脚本) 设置 身份验证令牌（token), 然后获取 http://yoursite.com/job/test/build?token=TOKEN_NAME 并复制

在 构建环境 里提供Node 环境 （需要安装Jenkins NodeJs 插件）


### 创建harbormaster 构建计划

在 Phabricator 上找到 ` Applications` -> `Harbormaster` -> `Build Plans` -> `Create Build Plan` 进入创建构建计划页面

选中 `Add Build Step` 进入构建步骤 找到 `Make an HTTP request` 设置URI填写上面复制的url`http://yoursite.com/job/test/build?token=TOKEN_NAME ` , 请求方法设置 `Post` ,  然后新增一个 Credentials 用来登录Jenkins 的账户名和密码，密码使用在Jenkins用户配置页面下 找show API Token 。 点击 `Create Build Step ` 完成创建


### 创建herald 通知规则

在 Phabricator 上找到 ` Applications` -> `Herald` -> `Create Herald Rule`

在 New Rule for 选中 `Commits` 规则，这个能够监听到 `git push`的请求

在 Rule Type 选中 `Global` 规则，提交后进行对应条件的添加

在 `Conditions` 中设置 Repository 是  `repository name`

在 `Action` 中 设置 Run build plans 选中上面设置的 build plans, 到此设置已经完成


接下来， 我们在把刚才的 git 库 clone 到本地，通过用 `hexo init` 一个 hexo 项目，然后跟着 [用 hexo 和 github 搭建静态博客系统](http://blog.haohuan.org/posts/201804/github-hexo/) 把配置文件改完，然后在jenkins 上写上需要执行的脚本的，现在只要你在本地的git 库push 到远程的git库时 这样子只要你更新了博客内空就会自动更新同步到你的博客了，不需要你去理会其他更多的构建发布步骤了


### 常见问题

> Jenkins RestAPI调用出现Error 403 No valid crumb was included in the request

方法一（不推荐）：

在jenkins 的Configure Global Security下 , 取消“防止跨站点请求伪造（Prevent Cross Site Request Forgery exploits）”的勾选

方法二：

1、获取用户API token

http://Jenkins_IP:8080/user/username/configure

点击 show API Token，假设是API_TOKEN

2、计算CRUMB

```bash
CRUMB=$(curl -s 'http://USER:API_TOKEN@Jenkins_IP:8080/crumbIssuer/api/xml?xpath=concat(//crumbRequestField,":",//crumb)')

```

3、请求时附带CRUMB信息即可

```bash
curl -X POST -H "$CRUMB" http://USER:API_TOKEN@Jenkins_IP:8080/reload
```

> jenkins 执行 hexo deploy  出现 `host key verification failed`

在 /var/lib/jenkins/.ssh/known_hosts 文件中添加  

```bash
github.com,192.30.255.112 ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAq2A7hRGmdnm9tUDbO9IDSwBK6TbQa+PXYPCPy6rbTrTtw7PHkccKrpp0yVhp5HdEIcKr6pLlVDBfOLX9QUsyCOV0wzfjIJNlGEYsdlLJizHhbn2mUjvSAHQqZETYP81eFzLQNnPHt4EVVUh7VfDESU84KezmD5QlWpXLmvU31/yMf+Se8xhHTvKSCZIFImWwoG6mbUoWf9nzpIoaSjB+weqqUUmpaaasXVal72J+UX2B+2RPW3RcT0eOzQgqlJL3RKrTJvdsjE3JEAvGq3lGHSZXy28G3skua2SmVi/w4yCE6gbODqnTWlg7+wC604ydGXA8VJiS5ap43JXiUFFAaQ==
```
