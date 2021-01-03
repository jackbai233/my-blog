---
layout:     post
title:      "Linux下MySQL8.0修改初始密码"
subtitle:   ""
description: "主要讲述了怎样修改MySQL8.0的初始密码"
date:       2020-05-26
author:     "JackBai"
published: true
tags:
    - Linux
    - MySQL
---
以下讲述了怎样修改MySQL8.0的初始密码。

<!--more-->
## 背景
在安装完MySQL后，使用如下命令
```shell
sudo service mysql start
```
启动mysql服务后，再使用登陆命令
```shell
mysql -u root -p
```
时根据提示，无论尝试输入什么密码都报错。看网上大多的都是先在配置文件中加入 *skip-grant-tables* 参数，然后重启mysql服务，使得mysql能无密码登入，然后再使用命令来设置mysql密码，但是设置密码的这个命令中因为有 *password()*函数，结果在MySQL8.0版本后就会报错，因为这个版本下已经没有password或password()函数了。
## 操作
经过参考，最后使用了一下方法成功修改了root密码。
首先找到原始的mysql账户和密码，我在本机的 **/etc/mysql/debian.cnf** 文件中找到了对应信息：
![获取初始用户密码](https://img-blog.csdnimg.cn/20200526232101499.png)

然后使用改账户与密码登陆进mysql
```shell
 mysql -udebian-sys-maint -pJge19hvTiwgZJw9n
```
![进入mysql服务](https://img-blog.csdnimg.cn/20200526232137367.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3hpYW9iYWlfb2w=,size_16,color_FFFFFF,t_70)
然后输入如下密令成功为root用户更改了密码：
```shell
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

提示：将上面命令中的password单词换成自己的密码，另外，在输入新密码的时候，由于MySQL的规则，可能密码需要进行大小写混合组成。
## 参考：
[https://blog.csdn.net/weixin_43530726/article/details/91303898](https://blog.csdn.net/weixin_43530726/article/details/91303898)
[https://newsn.net/say/mysql8-password.html](https://newsn.net/say/mysql8-password.html)
[https://my.oschina.net/u/4283151/blog/4122994](https://my.oschina.net/u/4283151/blog/4122994)