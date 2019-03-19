---
title: webStorage-cookie
date: 2018-03-02 11:06:36
tags:
  - '缓存'
  - 'cookie'
---

本文主要是对比浏览器中的 webStorage 和 cookie 区别

## WebStorage
Web Storage 的目的是克服由cookie 带来的一些限制，当数据需要被严格控制在客户端上时，无须持续地
将数据发回服务器。主要的目的是一是能提供一种在cookie之外存储会话数据的途径；二是提供一种存储大量
可以跨会话存在的数据的机制。

## Cookie
 cookie 全名叫 HTTP Cookie，通常直接叫做 cookie，最初是在客户端用于存储会话信息的。

||||
|---|---|---|
||WebStorage| Cookie|
|构成|key-value 对象|一个键值对形式的字符串 包含名称(name)(必要)，值(value)(必要)，域(domain)，路径(path)，失效时间(expires)，安全标识等可选属性|
|作用域|必须来自同一个域名（子域名无效）,使用同一种协议，在同一个端口上|绑定在指定的域名(domain)，可以设置不同路径(path)访问|
|存储空间大小|不同浏览器有区别，一般是 5MB的限制| 4KB 限制|
|数量限制||不同浏览器会有不同限制，safari和chrome 没有硬性规定|
|值的类型|字符串|字符串（通常需要通过encodeURIComponent()来保证它不包含任何逗号、分号或空格(cookie值中禁止使用这些值)|
|有效期|localStorage 无期限, sessionStorage页面会话结束时会被清除|通过expires 属性来指定|
