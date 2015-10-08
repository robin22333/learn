---
layout: post
title: Git 学习笔记
---
### 安装git
#### 安装
```bash
$ yum install git
```
不同的操作系统安装的方法不一样，我使用的是Fedora19 kde，具体可参考官方的安装手册[Git Download](http://www.git-scm.com/download/)
#### 配置
```bash
$ git config --global user.name "Robin"
$ git config --global user.email "luobin1105@gmail.com"
```
### 创建版本库
#### 初始化一个仓库
```bash
$ mkdir learngit
$ cd learngit
$ git init
```
#### 提交文件
```bash
$ git add <file>
$ git commit -m ""
```
-m后面输入的是本次提交的说明
#### 查看仓库当前的状态
```bash
$ git status
```
#### 查看文件修改内容
```bash
$ git diff <file>
```
### 版本回退
#### 查看提交日志
```bash
$ git log --pretty=oneline
```
--pretty=oneline用于过滤信息
#### 版本穿梭
在Git中，用HEAD表示当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。
```bash
$ git reset --hard commit_id
```
#### 查看命令历史
```bash
$ git reflog
```
### 撤销修改
#### 丢弃工作区的修改
```bash
$ git checkout -- <file>
```
命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：

1. readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

2. 是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次git commit或git add时的状态。
#### 丢弃暂存区的修改
```bash
$ git reset HEAD <file>
```
