---
layout: post
title:  "Linux系统tmux命令介绍"
date:   2019-07-25 23:10:00 +0800
author: 西伯利亚虎
categories: technical
---
远程使用linux时，在关闭ssh终端后，有时需要程序在远程继续运行，或希望下次远程登录后能够快速恢复上次工作的终端状态，这时tmux命令就派上了用场。

tmux命令管理终端有session、window、pane三个层次。在使用tmux管理终端时，以`Ctrl`+`B`为启用前缀（prefix）。

## Session层次的操作
* 新建一个session：`tmux new -s [session_name]`
* 在session内新建session（不会嵌套），除以上方式，还可以：`<prefix>:new -s [session_name]`
* 退出tmux：`<prefix>d`
* 列出所有session：`tmux ls`
* 进入某个session：`tmux at -t [session_name]`
* 删除某个session：`tmux kill-session -t [session_name]`
* 在session内删除当前session，除以上方式，还可以：`<prefix>:kill-session`
* 重命名当前session：`<prefix>$`+新session名（会有提示）
* 切换session：`<prefix>s`
* 关闭全部session：`tmux kill-server`

## Window层次的操作
* 新建一个window：`<prefix>C`
* 进入某个window：`<prefix>`+window数字
* 重命名当前window：`<prefix>,`+新window名（会有提示）
* 删除/退出一个window：`<prefix>&`或在该窗口所有pane中`exit`
* 切换/列出所有window：`<prefix>W`



## Pane层次的操作
* 垂直分割（分割为左、右两部分）：`<prefix>%`
* 关闭当前pane：`<prefix>x`（会提示y/n）或`exit`
* pane间切换：`<prefix>q`+pane数字（会有提示）
* 将当前pane在新window中打开：`<prefix>！`
* pane左右移动：`<prefix>{`和`<prefix>}`
* 采用下一个pane布局`<prefix><space>`
* 切换到上一次使用的pane：`<prefix>;`

