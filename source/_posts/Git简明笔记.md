---
title: Git简明笔记
img: 
top: false
cover: false
coverImg: 'https://cdn.jsdelivr.net/gh/rainbowtp/blog_photo/'
toc: true
mathjax: false
author: rainbow
date: 2020-04-19 00:12:59
password:
summary: git常用命令
categories:
  - 工具
tags:
  - git
---

# Git commands

## operation

### 用户名
`git config --global user.name "Firstname Lastname"`
### 邮箱
`git config --global user.email "your_email@example.com"`
### 代理
`git config --global https.proxy http://127.0.0.1:port`
`git config --global https.proxy https://127.0.0.1:port`
### 高亮
`git config --global color.ui auto`
### 生成ssh
`ssh-keygen -t rsa -C "your_email@example.com"`
### 初始化仓库
`git init`
### 暂存区添加文件
`git add`
` .` 覆盖型提交，排除删除文件  ` -u` 已被add的文件改动 `-A` 所有类型改动
### 暂存区快照
`git commit`
` -m "description"` 快捷添加简述
` --amend` 修改提交信息
### 切换分支
`git checkout branch`
` -b` 创建 ` -` 上一个分支 ` origin/branch` 分支远程来源
### 合并分支
`git merge branch`
` --no-ff` 保留原分支的commit历史 ` --squash` 原分支所有commit历史压缩为一个commit ` --no-commit` 防止合并失败，不自动提交
### 回溯版本
`git reset commit`
`--mixed` 重置索引，但不重置工作树，更改后的文件标记为未提交（add）的状态。默认操作。
` --hard` 重置索引和工作树，并且a分支修改的所有文件和中间的提交，没提交的代码都被丢弃了。
` HEAD` 当前版本 ` HEAD^` 上个版本 `HEAD~number` 往上第num个版本
### 合并提交历史
`git rebase -i HEAD-2` 合并连两个版本的提交
### 添加远程仓库
`git remote add origin url.git` 
### 推送到远程仓库
`git push origin branch`
` -u` 绑定pull远程仓库
### 拉取远程仓库
`git clone url.git`
` path` 保存目录 




## view

### 仓库状态
`git status`
### 提交日志
`git log` 当前状态为止
` --pretty=short` 只显示一行 ` filename` 选定文件的日志 ` -p` 带来的改动 ` --graph` 图形界面
`git reflog` 所有
### 版本差别
`git diff`
` HEAD` 与最新版本的差别
### 分支
`git branch`
` -a` 同时查看本地和远程分支