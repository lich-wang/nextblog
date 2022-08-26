---
title: Github Page, Hexo, Travis CI, VS Cdoe 最佳实践
---
# 介绍

## Github Page

[Github Page](https://pages.github.com/) 是GitHub提供的免费的静态网页托管服务, 只要创建一个和自己GitHub用户名相同的Project, 即可在 GitHub用户名.github.io 拥有一个网站, 非常适合用于作为个人博客网站使用.

使用 Github Page 作为个人博客有如下优势  
* 完全免费
* 依托 Github, 背后有微软投资，跑路风险小
* Greek, 或者说逼格够高
* 支持域名绑定

## Hexo

[Hexo](https://hexo.io) 是一个快速, 简洁且高效的博客框架. Hexo 使用 Markdown（或其他渲染引擎）解析文章, 在几秒内, 即可利用靓丽的主题生成静态网页.

使用 Hexo 作为 Github Page 博客系统有如下优势
* 官方支持 GitHub Page
* 有中文文档
* 支持 Markdown
  
<!-- more -->

## 那么代价是什么

直接使用 Github Page 和 Hexo 的缺点也很明显

* 过于Greek, 直接编辑发帖不方便
* Markdown 编写还是不直观
* Hexo 发布到 Github Page 依然有多个步骤

为了解决这个问题, 下面是我的最佳实践

## 工作流
```mermaid  
flowchart LR

A[VS code] -->|编辑| B[Hexo 源项目]
B -->|git push| C[Git 源项目]
C -->|Trave CI| D[Git Page 项目]

```
* 在 VS Code 使用 Remote SSH, Markdown Preview Enchanted, Markdown All in One 远程可视化编辑部署在Linux Service 上的 md 源文件
* 完成编辑后使用 VS Code 直接 commit 和 push 文章到GitHub源项目
* Github 上的源项目通过Travel CI 持续集成直接发布到GitHub Page项目

这样就可以实现所见即所得, 并且不同环境只要打开 VS Code 简单安装三个插件, 少量配置即可保持一致的文章发布体验.并且所有的配置和数据都在服务器. 任何情况都可以轻易恢复环境.

下面在正式开始环境搭建之前,需要做好如下准备.

## 准备

* github 账号
* 自由访问互联网
* 一台Linux service
  * 最好24小时运行
  * 实在没有虚拟机也可以


# Hexo on Linux

Ubuntu 为例

## 准备工作

- 更新系统
  

``` bash
sudo apt update
sudo apt upgrade
```

- 创建工作目录，后面所有操作默认在下面的目录执行
``` bash
mkdir nextblog
cd nextblog
```

## 安装Node.js

- 安装npm，依赖的node就自动安装了
``` bash
sudo apt install npm
```

- 安装后查看版本
``` bash
node -v
npm -v
```

## 安装HEXO

- 完整安装Hexo
``` bash
npm install -g hexo-cli
```
- 初始化 Hexo, 注意一定在新目录下.
``` bash
hexo init
npm install 
```
- 启动Hexo
```
hexo d
hexo s
```

## 配置NEXT主题
## 安装配置git
# GitHub Page project
# GitHub source project
# VS Code on Windows

# 恢复 Hexo on Linux
# 恢复 VS Code on Windows

## 下载安装VS Code
## 命令行生成密钥
``` PowerShell
ssh-keygen -t rsa -C "lichPC"
```
输出如下，其中“lichPC” 为注释，随便写
``` PowerShell
PS C:\Users\lich> ssh-keygen -t rsa -C "lichPC"
Generating public/private rsa key pair.
Enter file in which to save the key (C:\Users\lich/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in C:\Users\lich/.ssh/id_rsa.
Your public key has been saved in C:\Users\lich/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:HCWn15Tt33hWj6+kfgjptsWS7SpqbUA16c6mfZj7ZKo lichPC
The key's randomart image is:
+---[RSA 3072]----+
|        ..o .o   |
|        += o. .  |
|       oo.. ..   |
|      ...o    . .|
|     . oS  .   ++|
|      . + o+  o *|
|       * +=.+..+ |
|      o B+++.o. .|
|     .E+o*+++... |
+----[SHA256]-----+
```
## 查看，并复制公钥信息
``` PowerShell
cat ~\.ssh\id_rsa.pub
```
复制输出的内容
``` PowerShell
PS C:\Users\lich\.ssh> cat ~\.ssh\id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDIlqewgvVeHx8b0+KrO7ucL2ynXNrIEq+isG07rYR2rf4HYSbaDxWk9ZspGSp4zxzc1OZ+nraofeRnlCX2ijMc0RfUE9nf9qPq7/J08SbQ96dz/pbKb2h5MHKk3UIfq0+40ZOoPpGqVZ0/qJdthBM9DdwB4V/xjJlKZojgLJzy3XheGYjGSfoTJjHK9HfvRxFrJXnLG9Lh0tYRZ/KE6ox129KaSSabQswTRpArzkKe88WaBWu6rV31+FDRirJxXZZ6pN0IS4mXTRViNhMc4KXk3fO5LxDHRCX9tCzr+FLBpDrhr6+aK7zU6Ur6i7wXNzNIoBXnhldZyHUuCBARG5wN4g5AjrUzQPZF3hFyZzRDR9ZLCxK0mWN4VchBDqgx9ST38NibyKFnMjerPVPyng9MvKllkqUUqulwTatElH+IfwFocn31O+vIP7et0Eii3PtJWFDXDQTl7FLOEFO8qDHpm04+b3bRq1GlGJIKcu+JJXIX67fQKQzzcmQ9C2f22f8= lichPC
```

## 添加公钥到远程服务器

```bash
nano ~/.ssh/authorized_keys
```
粘贴公钥信息到最后一行

``` bash
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIO9INiHnEXicATPWzDpADnw3edvp+iEKhkopHaRpyTk8 lich.wang@gmail.com
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDiwY8yydjvuLfY78zxvPMoQyJQOwjnskOTH+Hbs7PTL8J+niZT7FSChTdNdBwVqA9EqAhht0/Adu+8LnbZIa78nk9qmfVEMyVmBhnaY1VlAb6nfNQ2PA3+YYZlhmn5j3Jc/WE2v7emUCxMhht+Ic4yZI5I34VLwKWrpzyhUmfRq0siifuIS0G9soIOb37dPyWBMqKutwXZ240KIz7VGGpRgIzEY4Wtelar4UqF8Whkl65RptWR325WeXRMQyW9gm5CayorYs9WDtHFOtDi4zwy6ioqy/cyypoGy8uXmMxU2DRMs+fEGvX4P4bPBGo+twvq0IagKmOzzPvQzUaXeDtBdS0tzGJC0FJxC7f5tRsWC+6Q7MnmVOPcmV74e9OgN5cNUcQnN8dk2zXm8NR4G54s3TM8wdtyBJolS3Zxhj3Bh0vJxyQSkMJoax6Bnccg9F+Br9x6cJJdrhy7rZfR4E8IfiQpqAsGI8u80c4j6K3fcWWCquW1/hO0GaQdoHt9uks= lich@DESKTOP-54AOQFI
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDIlqewgvVeHx8b0+KrO7ucL2ynXNrIEq+isG07rYR2rf4HYSbaDxWk9ZspGSp4zxzc1OZ+nraofeRnlCX2ijMc0RfUE9nf9qPq7/J08SbQ96dz/pbKb2h5MHKk3UIfq0+40ZOoPpGqVZ0/qJdthBM9DdwB4V/xjJlKZojgLJzy3XheGYjGSfoTJjHK9HfvRxFrJXnLG9Lh0tYRZ/KE6ox129KaSSabQswTRpArzkKe88WaBWu6rV31+FDRirJxXZZ6pN0IS4mXTRViNhMc4KXk3fO5LxDHRCX9tCzr+FLBpDrhr6+aK7zU6Ur6i7wXNzNIoBXnhldZyHUuCBARG5wN4g5AjrUzQPZF3hFyZzRDR9ZLCxK0mWN4VchBDqgx9ST38NibyKFnMjerPVPyng9MvKllkqUUqulwTatElH+IfwFocn31O+vIP7et0Eii3PtJWFDXDQTl7FLOEFO8qDHpm04+b3bRq1GlGJIKcu+JJXIX67fQKQzzcmQ9C2f22f8= lichPC
```

## VS code 添加远程服务
VS Code 安装 remote SSH 插件后,输入 ```   ssh pi@lich.tech -p 15001  ``` 连接服务器