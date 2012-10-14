
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
    git branch branch_name
    git checkout branch_name | git checkout master
    git merge branch_name
    git diff //查看冲突
    gitk //图形显示项目历史
    git branch -d local | git branch -D local //delete

##查看历史
    git log
    git log -p //显示patchs
    git log --stat //显示修改文件及添加删除了多少行
    git log --pretty=[raw|short|format] //格式化日志
    git log --pretty=format:'%h : %s' --graph

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
    git push 

##Git标签
   标签对象可以指向任何对象，但通常是一个提交(commit),而第一个是tree

    git tag tag-name commit_shavalue //轻量级，分支不移动
    git tag -a tag-name commit_shavalue //创建标签对象




//以下内容来自网络其它地方
##删除文件
    git rm filename1 filename2
    git rm -r fold/
    git commit -m 'rm file'
  
##重命名
    git mv old.txt new.txt

##生成变更日志
    git log > ChangeLog