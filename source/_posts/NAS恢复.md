---
title: NAS恢复
date: 2024-07-29 13:44:22
tags:
---

## 映射关系
|服务           |cloudflare domain          |cloudflare Port    |Server Port|
|----           |----------                 |----------         |-------    |
|路由控制台     |https://gw.lich.tech       |880                |N/A        |
|Linux(ssh)     |N/A                        |222                |22         |
|网盘(nextcloud)|https://pan.lich.tech      |8443               |8443       |
|书籍(calibre)  |https://book.lich.tech     |583                |8083       |
|下载(qbit)     |https://qbit.lich.tech/    |588                |8080       |
|电影(radarr)   |https://movie.lich.tech/   |7878               |7878       |
|剧集(sonarr)   |https://tv.lich.tech/      |8989               |8989       |
|种子(jackett)  |N/A                        |                   |9117       |
|影音(ombi)     |N/A                        |                   |3579       |
|字幕(bazarr)   |N/A                        |                   |           |
|动漫(bangumi)  |N/A                        |                   |7892       |
|SMB            |                           |
|gitlab         |                           |
|drawio         |                           |
|plantuml       |
|nginx          |
|certbot        |
|watchtower     |
|homeassistant  |

## 系统恢复
### SSH
#### 恢复私钥文件
#### 恢复authorized_keys
``` bash
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDIlqewgvVeHx8b0+KrO7ucL2ynXNrIEq+isG07rYR2rf4HYSbaDxWk9ZspGSp4zxzc1OZ+nraofeRnlCX2ijMc0RfUE9nf9qPq7/J08SbQ96dz/pbKb2h5MHKk3UIfq0+40ZOoPpGqVZ0/qJdthBM9DdwB4V/xjJlKZojgLJzy3XheGYjGSfoTJjHK9HfvRxFrJXnLG9Lh0tYRZ/KE6ox129KaSSabQswTRpArzkKe88WaBWu6rV31+FDRirJxXZZ6pN0IS4mXTRViNhMc4KXk3fO5LxDHRCX9tCzr+FLBpDrhr6+aK7zU6Ur6i7wXNzNIoBXnhldZyHUuCBARG5wN4g5AjrUzQPZF3hFyZzRDR9ZLCxK0mWN4VchBDqgx9ST38NibyKFnMjerPVPyng9MvKllkqUUqulwTatElH+IfwFocn31O+vIP7et0Eii3PtJWFDXDQTl7FLOEFO8qDHpm04+b3bRq1GlGJIKcu+JJXIX67fQKQzzcmQ9C2f22f8= lichPC
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIO9INiHnEXicATPWzDpADnw3edvp+iEKhkopHaRpyTk8 lich.wang@gmail.com
```
### frpc
``` bash
# frpc.ini
[common]
server_addr = lich.tech
server_port = 7000

[ssh]
type = tcp
local_port = 22
remote_port = 222
```

### Github
``` bash
git config --global user.email "lich.wang@gmail.com"
```
## 影音服务

## 博客

## 代码