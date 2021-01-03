---
layout:     post
title:      "Go设置代理--windows系统"
subtitle:   ""
description: "主要介绍在windows下配置go的代理环境以能正确拉取go下的相关包"
date:       2020-05-29
author:     "JackBai"
published: true
tags:
    - Golang
    - Proxy
---
下文主要介绍在windows下配置go的代理环境以能正确拉取go下的相关包。

**注意，下面的步骤适合于1.13版本以上的Go环境**
## 步骤
1. 在安装完Go环境后，在GOPATH的src目录下创建 **goland.org/x/** 目录，进入此目录，执行命令：
```shell
$ git clone https://github.com/golang/tools.git
$ git clone https://github.com/golang/lint.git
```
> 注意：直接在https://github.com/golang/tools 网址界面download这个tools-master包解压后的大小，没有clone下来的tools文件夹大，所以建议直接clone下来。

2. 将Go默认的代理替换为以下代理：
```shell
go env -w GOPROXY=https://goproxy.cn,direct
```
3. 对VsCode进行设置，如果平时有代理，一定要先设置代理，在VsCode中，根据“文件->首选项->设置”打开,然后搜索 "http.proxy"关键字，找到Http:Proxy 这一行，在里面填入自己的代理服务器，例如：
```
http:proxy.com.cn:8080
```
4. 在VsCode中随意打开一个go格式文件，VsCode右下角会出现一些提示让你安装一些工具，直接点击Install All即可。

题外话，若在有代理的情况下，在windows下使用go modules下载包时还需要配置代理，具体参考[这个](https://zcdll.github.io/2018/01/27/proxy-on-windows-terminal/)。若嫌每次打开窗口都要设置的话，可以将这几个代理参数放到系统环境变量里面。