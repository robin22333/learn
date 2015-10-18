# Git 学习笔记
首先推荐廖雪峰老师的[Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b00)，浅显易懂，适合新手学习。该笔记就是廖老师的教程的学习整理。
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
### 文件删除
首先删除文件
```bash
$ rm -f <file>
```
这个时候，Git知道你删除了文件，因此，工作区和版本库就不一致了,现在你有两个选择，一是确实要从版本库中删除该文件，那就用命令git rm删掉，并且git commit：
```bash
$ git rm <file>
$ git commit -m ""
```
另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：
```bash
$ git checkout -- <file>
```
### 远程仓库
首先登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库：learngit
#### 把本地仓库与之关联
```bash
$ git remote add origin git@github.com:robin22333/learngit.git
```
#### 把本地库的所有内容推送到远程库上
```bash
$ git push -u origin master
```
由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关来，在以后的推送或者拉取时就可以简化命令。
```bash
git push origin master
```
#### 从远程库克隆
```bash
$ git clone git@github.com:robin22333/learngit.git
```
### 分支管理
#### 创建与合并分支
创建分支
```bash
$ git checkout -b dev
```
git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：
```bash
$ git branch dev
$ git checkout dev
```
然后，用git branch命令查看当前分支：
```
$ git branch
```
git branch命令会列出所有分支，当前分支前面会标一个*号。
切换回master分支
```bash
$ git checkout master
```
合并分支
```bash
$ git merge dev
```
git merge命令用于合并指定分支到当前分支

删除分支
```bash
$ git branch -d dev
```
通常合并分支时候，Git会使用Fast-forward方式，即“快进模式”，也就是直接把master指向dev的当前提交，所以合并速度非常快，但这种模式下，删除分支后，会丢掉分支信息。

如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
```bash
$ git merge --no-ff -m "" dev
```
因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。
#### Bug分支
修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。
#### future分支
删除一个未合并的分支
```bash
$ git branch -D <name>
```
####
```bash
$ git remote -v
```

