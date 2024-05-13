---
title: 如何优雅的解决hexo粘贴图片问题
date: 2024-05-13 23:15:11
tags:
---
* 最新版VS Code在md文件中粘贴图片的时候，会自动默认上传文件到md文件同名文件夹下,同时会自动生成MD格式的链接，这个路径是可以设置的
* hexo 有推荐用[hexo-renderer-marked](https://hexo.io/docs/asset-folders#Embedding-an-image-using-markdown)来改变路径
* 但是这个和VScode的预览机制不同,github上有一个[临时解决方案](https://github.com/hexojs/hexo-renderer-marked/issues/216)，和以一个[正式方案](https://github.com/hexojs/hexo-renderer-marked/pull/271)在等待合并。

我的方案是，把修改后的js复制出来，在部署前复制回去，具体变更在[这个MR](https://github.com/lich-wang/nextblog/commit/2ec99faa7282f3b31ce80b8f99996a84c2fb814d)

PS: VS code 配置

```json
    "markdown.copyFiles.destination": {
        "**/*.md": "${documentDirName}/${documentBaseName}/${fileName}"
    }
```
