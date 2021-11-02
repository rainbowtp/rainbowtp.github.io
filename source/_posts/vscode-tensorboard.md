---
title: vscode tensorboard
author: rainbow
top: false
cover: false
toc: true
mathjax: true
date: 2021-11-02 10:13:07
tags:
 - 疑难杂症
categories:
 - 工具
summary:
 vscode内置的tensorboard组件启动报错
img:
coverImg:
password:
---

 vscode内置的tensorboard组件启动时报错:

```txt
启动 TensorBoard 会话失败，错误：Error: Timed out after 60 seconds waiting for TensorBoard to launch.
```

我首先在google上找到的首个帖子是几年之前的bug,现在已经完全修复

之后完全没有思路 因为不知道这个组件是怎么实现的

在[这个](https://stackoverflow.com/questions/55690274/attributeerror-module-numpy-has-no-attribute-integer-getting-this-error)回答里找到灵感

tensorboard组件其实就是终端输入命令 然后将服务和html集成到vscode本身

你可以直接在vscode的输出栏里debug

我的问题是 没有选择对python路径

这个路径是tensorboard失败报错后才可以选的 此外conda的相关设置也会重置
