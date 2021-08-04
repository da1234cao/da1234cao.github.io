---
title: 使用hexo+github搭建个人博客
date: 2021-08-04 16:11
categories: 
- 杂项知识点
tags:
- git
- hexo
excerpt: 使用hexo+github搭建个人博客。
---

## 挑选一个主题

在[themes](https://hexo.io/themes/)中，挑选一个主题。我目前选择的是[fluid](https://github.com/fluid-dev/hexo-theme-fluid)

<br>

## 使用Hexo搭建本地博客

准备[Hexo](https://hexo.io/zh-cn/docs/)安装环境。

* [nodejs](https://nodejs.org/zh-cn/docs/)：作为一个异步事件驱动的 JavaScript 运行时，Node.js 被设计用来构建可扩展的网络应用。
* [npm](https://docs.npmjs.com/about-npm)：node包管理器。是Node.js默认的、用JavaScript编写的软件包管理系统。

```shell
sudo apt install nodejs
sudo apt install npm
node --version
```

升级nodejs版本，否则后面会存在[这个](https://stackoverflow.com/questions/67516168/i-just-installed-hexo-static-site-generator-on-debian-and-ran-hexo-server-to-see)报错。

```shell
# 我没看这两条命令的具体作用是什么，但确实管用。
sudo npm install n -g
sudo n stable
node --version
```

全局安装Hexo。

```shell
sudo npm install -g hexo-cli
```

本地建站并启动。

```shell
# 请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。
hexo init <folder>
cd <folder>
npm install

$ hexo generate/g  # 载入全部.md文件，生成可供浏览器展示的HTML静态页面
$ hexo server/s  # 将本机作为托管服务器，在本地启动站点，可通过 localhost:4000 访问博客
```

<br>

## 替换主题

根据[hexo 配置](https://hexo.io/zh-cn/docs/configuration)和[fluid](https://github.com/fluid-dev/hexo-theme-fluid)的为文档，修改配置文件即可。

很多我还没该，暂时可以上传文章即可。

```shell
# 安装fluid主题
npm install --save hexo-theme-fluid

# 配置config文件
...

# 安装git插件
npm install hexo-deployer-git --save
```



<br>

### 多机同步



<br>

## 写博客

避免我忘记，这里记录下。

```shell
hexo generate
hexo deploy
```



## 参考

[Ubuntu + GitHub Pages + Hexo 搭建个人博客](http://dongdongdong.me/2018/01/25/OS/Installation/Ubuntu/blog-github-hexo/)