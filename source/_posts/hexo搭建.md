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
## 安装Node.js
## 安装HEXO
## 配置NEXT主题
## 安装配置git
# GitHub Page project
# GitHub source project
# VS Code on Windows

# 恢复 Hexo on Linux
# 恢复 VS Code on Windows