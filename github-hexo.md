---
title: 用 hexo 和 github 搭建静态博客系统
date: 2017-04-18 23:30:54
tags:
  - 'git'
---

许多人都希望自己有一个博客，但有时会觉得要搭个博客很繁琐，需要各种各样的环境，其中不知道还会出现什么错误信息，如果你曾经或者现在正有这样的想法，只要你跟着这篇文章动手起来，很快就能让你快速拥有自己的博客网站，记录生活的点滴。

<!-- more -->

### 环境准备
  + Git
  + NodeJs

### 配置github
  + 有一个github 账号
  + 建立一个与你用户名对应的仓库，eg: yourUserName.github.io
  + 配置ssh-key

### 安装hexo

  + 安装

  ```bash
  # npm install -g hexo-cli
  ```
  + 初始化Hexo
  在你的PC上建立一个文件夹 `<folder>`

  ```bash
  # hexo init <folder>
  # cd <folder>
  # npm install
  ```

  + 启动服务

  ```bash
  # hexo server
  [info] Hexo is running at http://localhost:4000/. Press Ctrl+C to stop.
  ```

  这样在本地就能看到你的blog了, 这样就能在本地调试你的blog了

### 本地调试

   ```bash
   # hexo new "newPost" 新建文章
   # vim newPost.md  编辑文章
   # hexo new page "pageName" #新建页面
   # hexo generate #生成静态页面至public目录
   # hexo server #启动本地服务，进行文章预览调试
  ```

### 配置并发布

  + 新建一篇文章

  ```bash
  # hexo new "My New Post"  //会在目录下生成 source\_posts\My-New-Post.md
  ```
  > 可以用 `markdown` 语法来编写你的文章

  + 配置_config.yml
    找到下面的内容
      ```bash
      ...

      # Deployment
      ## Docs: http://hexo.io/docs/deployment.html
      deploy:
        type:
      ```
      把它们修改为

      ```bash

      ...
      # Deployment
      ## Docs: http://hexo.io/docs/deployment.html
      deploy:
        type: git
        repository: git@github.com:yourUserName/yourUserName.github.io.git
        branch: master

      ```
      > 注意：
      repository: 必须是SSH形式的url
      eg: `git@github.com:yourUserName/yourUserName.github.io.git`
      而不能是HTTPS形式的url
      `https://github.com/yourUserName/yourUserName.github.io.git`，否则会出现错误
      如果你是为一个项目制作网站，那么需要把branch设置为gh-pages。

  + 发布

   ```bash
   # hexo deploy
   ```

### 添加自定义域名解释
   * 把域名用CNAME的方法解析到 yourUserName.github.io.git.
   * 在source文件夹里添加CNAME文件并添加你自己的域名

   ```bash
   xxx.yyy.zzz
   ```

### 日常部署步骤
  ```bash
  # hexo clean
  # hexo generate
  # hexo deploy
  ```

###  添加“Fork me on Github” ribbon
  打开这个[ribbon](https://github.com/blog/273-github-ribbons) 把a 标签的代码粘贴到 `themes\next\layout\layout.xxx` 中，放置在 最后，标签</body>之前即可，记得修改你的github
  地址
### 常见错误

  + 执行 hexo deploy 后,出现 error deployer not found:github 的错误
    > hexo 更新到3.0之后，deploy的type 的github需要改成git, 接着
      npm install hexo-deployer-git --save 改了之后执行，然后再部署
