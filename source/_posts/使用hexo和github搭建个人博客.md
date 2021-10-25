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

master分支用于展示网页。doc分支用于存储内容。

每次操作之前同步doc，操作结束之后，重新生成并`hexo generate`更新master。

A主机操作：

```shell
$ git init
$ git checkout -b doc 
$ git add .
$ git commit -m "create a new branch for coordination among multiple devices" 
$ git remote add origin git@github.com:da1234cao/da1234cao.github.io.git
$ git push origin doc 
```

在电脑B处拉取分支doc，做更新博客操作，先需搭建环境：

```shell
$ git clone -b doc https://github.com/username/username.github.io.git
$ cd username.github.io
$ npm install # 安装依赖
```

此后就可以在电脑B上编辑更新博文了。

第五步：编译博客，将静态文件发布到主分支 **master** 上，源文件提交到分支 **doc** 上：

```shell
$ hexo clean && hexo g && hexo d
$ git add .
$ git commit -m "message"  # 源文件提交到hexo分支上面
$ git pull origin doc     # 先拉取原来GitHub的doc分支上的源文件到本地，进行合并
$ git push origin doc     # 比较解决前后版本冲突后，push源文件到GitHub的doc分支
```

第六步：再次回到电脑A进行博文编辑工作，同步hexo分支源文件到本地，进行合并：

```shell
$ git pull origin hexo
# 写好博文，重复操作第五步
```

## 文档插入图片

我不喜欢图床。我喜欢图片和文档在一个地方存储。参考：[Hexo博客搭建之在文章中插入图片](https://yanyinhong.github.io/2017/05/02/How-to-insert-image-in-hexo-post/)

绝对路径：可以将图片统一放在source/images文件夹中，通过markdown语法访问它们。

```shell
![](/images/image.jpg)
```

![喵喵](/images/使用hexo和github搭建个人博客/hexo_page_image.jpeg)

## 添加评论功能

参考：[给博客增加评论功能](https://drinkwd.github.io/2021/02/22/%E7%BB%99%E5%8D%9A%E5%AE%A2%E5%A2%9E%E5%8A%A0%E8%AF%84%E8%AE%BA%E5%8A%9F%E8%83%BD/)，我们给博客添加评论功能。

```shell
post:
  comments:
    enable: true
    type: utterances

utterances:
  repo: da1234cao/da1234cao.github.io
  issue-term: title
  theme: github-light
  crossorigin: anonymous
```

## 写博客

避免我忘记，这里记录下。

```shell
hexo generate
hexo deploy
```



## 参考

[Ubuntu + GitHub Pages + Hexo 搭建个人博客](http://dongdongdong.me/2018/01/25/OS/Installation/Ubuntu/blog-github-hexo/)