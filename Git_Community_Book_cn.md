Git Community Book中文版
============================

## Git对象模型

  SHA: 表示项目历史信息的文件，通过一个40个字符的"对象名"来索引。

### 对象

  三个部分：类型、大小和内容

  分四个类型: blob, tree, commit, tag

  * blob: 存储文件数据
  * tree: 管理tree和blob
  * commit: 指向一个tree，标记项目某特定时间点的状态
  * tag: 标记一个commit的方法

### 命令

  * git ls-tree tree_sha1; 
  * git show blob_sha1; 
  * git log , git show -s --pretty=raw commit_sha1;
  * git cat-file tag v1.5;
  
##Git目录与工作目录

  Git目录

  工作目录

##Git索引：工作目录和项目仓库间的暂存区。提交的是索引里的内容。
  
  > git status


##安装Git
  
  * linux:
    $ yum install git-core
    $ apt-get install git-core
  
  * Windows:
  
    下载安装msysGit

##配置
    
    git config --global user.name 'yourname'
    git config --global user.email 'your email'


##基本用法
  
    git clone git://git.kernel.org/pub/scm/git/git.git
    git clone http://www.kernel.org/pub/scm/git/git.git

    git init
    git add file1 file2 | git add .
    git diff --cached
    git status
    git commit -m 'commit' | git commit -a

##分支与合并基础

    git branch
    git branch -r // 查看远程分支
    git branch -a // 查看所有分支
    git branch branch_name
    git checkout -b newBranch //创建新分支
    git checkout branch_name | git checkout master
    git push origin newBranch
    git push origin --delete master  //删除远程分支
    git branch -d local | git branch -D local //删除本地分支
    git merge branch_name
    git diff //查看冲突
    gitk //图形显示项目历史
    
    # 迁出某个commit 
    git log
    git checkout commit_sha1 

##查看历史
    git log
    git log -p //显示patchs
    git log --stat //显示修改文件及添加删除了多少行
    git log --graph --oneline
    git log --pretty=[raw|short|format] //格式化日志
    git log --pretty=format:'%h : %s' --graph
    git log --author=Andy
    git log --grep="something in the message"
    git log [filename]
    git log branch1 branch2 ^master //查看在branch1, branch2但不在master分支上的提交
    
    
  

##比较提交
    git diff
    git diff --cached //显示当前索引和上次提交的差异

##分布式工作流程
    git clone
    git pull //直接合并远程分支
    git remote add bob /home/bob/myrepo
    git fetch bob //抓取远程文件但不合并
    git log -p master..bob/master //查看远程分支历史记录
    git merge bob/master //合并远程分支
    git push | git push origin master

##Git标签
   标签对象可以指向任何对象，但通常是一个提交(commit),而第一个是tree

    git tag tag-name commit_shavalue //轻量级，分支不移动
    git tag -a tag-name commit_shavalue //创建标签对象


//以下内容来自网络其它地方
##删除文件
    git rm filename1 filename2
    git rm -r fold/
    git commit -m 'rm file'
    git clean -n   // 显示将要删除的文件和目录
    git clean -df  // 删除（没有git add的）文件和目录
  
##重命名
    git mv old.txt new.txt

##生成变更日志
    git log > ChangeLog

##远程仓库相关
    查看远程仓库：$ git remote -v
    查看远程仓库：$ git remote show origin
    添加远程仓库：$ git remote add [name] [url]
    删除远程仓库：$ git remote rm [name]
    修改远程仓库：$ git remote set-url --push[name][newUrl]
    拉取远程仓库：$ git pull [remoteName] [localBranchName]
    推送远程仓库：$ git push [remoteName] [localBranchName]

## 备份工作区
    git stash save {name}
    git stash list
    git stash apply stash@{1}
    git stash pop
    git stash clear

##恢复命令
    git reset --mixed 此为默认方式，不带任何参数的git reset，即时这种方式，它回退到某个版本，只保留源码，回退commit和index信息
    git reset –soft：回退到某个版本，只回退了commit的信息，不会恢复到index file一级。如果还要提交，直接commit即可
    git reset –hard：彻底回退到某个版本，本地的源码也会变为上一个版本的内容
    eg: git reset –-hard HEAD~3 //向前回退到第3个版本

## 比较
* git diff master..test   // 比较两个分支差异
* git diff HEAD -- ./lib  // 限定比较目录

## 追踪分支
* git branch --track [name] origin/[name]

## 查找
* git grep -n [string]
* git grep --name-only [string]
* git grep -e '[string_a]' --and -e [string_b] // AND
* git grep --all-match -e '[string_a]' -e [string_b] // OR

## 撤消
* git revert HEAD
* git revert HEAD^

## 忽略文件
* .gitignore 项目公共忽略文件
* .git/info/exclude 项目私有忽略文件
* ~/.gitignore_global 或 /User/{xxx}/Document/.gitignore_global 全局忽略文件

## 维护Git
* git gc   // 压缩历史信息来节约磁盘和内存空间，此操作比较耗时
* git fsck // 运行仓库的一致性检查，此操作比较耗时

## 建立公共仓库
* git clone --bare [name] [name].git

## 定制GIT
* 更改编辑器 git config --global core.editor vim
* 添加别名 git config --global alias.las 'cat-file commit HEAD'
* 添加颜色 git config color.ui | color.diff auto
* 提交模板 git config commit.template '/etc/git-commit-template'
* 日志格式  git config format.pretty oneline

## 恢复已删除分支
* git fsck --lost-found
* git show [hash]
* git rebase [hash] | git merge [hash]

## 其它
* 添加本地忽略列表  echo '忽略文件名' >> .git/info/exclude
* git添加空文件夹：在文件夹中添加一个.gitkeep文件
* 退回到git add上一步：git rm -r --cached .


## FAQ
* fatal: Unable to create ‘/.git/index.lock’: File exists.
  - rm -rf /.git/index.lock