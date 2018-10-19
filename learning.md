# git

### git 入门
- git init 
    + 初始化这个仓库，同时也是构建这个git仓库
- git add
    + 添加文件到git仓库，可以add多个文件
```
git add file1
git add file2 file2
```
- git commit
    + 提交文件至仓库，这个提交是吧之前add的所有文件提交，是一次性提交
    + -m 参数：添加本次提交说明
```
git commit -m "three files"
```

### 版本管理
- git status
    + 用于查看当前仓库状态
- git diff
    + 用于查看仓库文件有什么变换,也就是有什么不同的地方
- git log
    + 用于查看当前仓库日志，最近到最远提交日志
    + --pretty=oneline 参数：精简一行显示
```
$ git log --pretty=oneline
686229f429e4b4787bf104495451f169fa188b0d (HEAD -> master) add nothing to README
cdee807ccf3ca37ff10397169c0d489cef2a70b3 add learing.md, modify README
d35a127f7daac624c7582e7f70b01bf615a0a882 add README
```
- HEAD 当前版本，HEAD^ 上一个版本，HEAD^^ 上两个版本，HEAD~n 上n个版本
- git reset
    + 当需要回退至某个版本，使用该命令
    + --hard 参数：
```
$ git reset --hard HEAD^
HEAD is now at cdee807 add learing.md, modify README

$ git log
commit cdee807ccf3ca37ff10397169c0d489cef2a70b3 (HEAD -> master)
Author: Silvester98 <1539168414@qq.com>
Date:   Sat Oct 13 20:51:51 2018 +0800

    add learing.md, modify README

commit d35a127f7daac624c7582e7f70b01bf615a0a882
Author: Silvester98 <1539168414@qq.com>
Date:   Sat Oct 13 20:31:42 2018 +0800

    add README
```
如上，现在回到了第二个版本。

现在要回到最新版本如何回去？——同样使用git reset 命令，只是最后接最新版本的commit id，同时，上面的命令行窗口还没有被关掉！
```
$ git reset --hard 68622
HEAD is now at 686229f add nothing to README

$ git log --pretty=oneline
686229f429e4b4787bf104495451f169fa188b0d (HEAD -> master) add nothing to README
cdee807ccf3ca37ff10397169c0d489cef2a70b3 add learing.md, modify README
d35a127f7daac624c7582e7f70b01bf615a0a882 add README
```
假如关掉命令窗口，不知commit id，使用如下命令：git reflog

- git reflog
    + 记录你的每一次命令，这样就可以查看之前命令，得知commit id
```
$ git reflog
686229f (HEAD -> master) HEAD@{0}: reset: moving to 68622
cdee807 HEAD@{1}: reset: moving to HEAD^
686229f (HEAD -> master) HEAD@{2}: commit: add nothing to README
cdee807 HEAD@{3}: commit: add learing.md, modify README
d35a127 HEAD@{4}: commit (initial): add README
```
- git checkout
    + -- file 参数：--不可少，用于工作修改想要撤回即直接丢掉工作区修改，此时还未添加到暂存区
- git reset HEAD file
    + 用于修改已提交至暂存区，这时使用该命令，撤销暂存区，返回至工作区。之后可以再使用git checkout -- file命令撤销修改
- git rm
    + 删除文件后，使用该命令，之后再commit，这个文件算是删除了
    + 如果说删错了，还未提交，那么可以使用 git checkout -- file 返回删除前的状态
    + 如果已经提交，那么可以版本回退

### 远程仓库
- git remote add origin remote-address
    + 将本地库与远程库关联
    + 关联后使用 git push -u origin master 第一次推送master分支所有内容
    + 之后就可以使用 git push origin master 推送更新修改
- git clone
    + 一般我们先在远程服务器创建一个仓库，之后使用该命令将远程库下载在本地，之后本地修改，再推送

### 分支管理
master 分支，为主分支，一开始，master分支是一条线，HEAD指向master分支，就能确定当前分支，以及当前分支提交点。

新建一个分支 dev，Git会新建一个dev指针，指向master相同提交，再把HEAD指向dev,表示当前分支在dev上。

之后就是对dev分支进行操作，以后每次commit,只有dev分支会前进，master分支不动.dev分支工作完成后需要与master分支合并，最简单的方法就是让master指针指向dev。之后也可以将dev分支删除，这样就只剩下master分支了。

- git checkout -b branch-name
    + 用于创建分支，-b参数就是创建分支，并切换至这个分支
```
$ git checkout -b dev
Switched to a new branch 'dev'
M       learning.md

相当于
$ git branch dev
$ git checkout dev
```
- git branch
    + 查看当前分支
```
$ git branch
* dev
  master
```

然后提交修改，切换到master分支，可以发现之前修改都没有了。因为分支回到了master分支，在dev分支上的修改就不会显示。

- git merge
    + 该命令是将指定分支合并到当前分支
    + 所有如果要合并到master分支需要先回到master分支
```
$ git merge dev
Updating dc661af..937db3e
Fast-forward
 learning.md | 38 ++++++++++++++++++++++++++++++++++++++
 1 file changed, 38 insertions(+)
```
- git branch -d branch-name
    + 合并之后就可以将分支删除，使用该命令
```
$ git branch -d dev
Deleted branch dev (was 937db3e).

$ git branch
* master
```
- git branch branch-name
    + 创建分支
- git checkout branch
    + 切换分支
- git log --graph
    + 查看分支图
    + 当合并发生冲突时，首先解决冲突，之后再进行合并
- git stash
    + 保存工作现场，对当前工作还未完成，也未提交，但是要转向别的分支，此时可以使用该命令保存现场，之后在返回此分支进行工作
    + git stash apply：恢复工作现场，但是stash中的内容并未删除，还需使用git stash drop 来删除
    + git stash pop：该命令相当于git stash apply 和 git stash drop
    + git stash list：查看当前保存的stash列表
- git branch -D branch-name
    + 强行删除一个还未合并的分支
- git remote
    + 查看远程库信息
    + -v参数 详细查看
- git push origin branch-name
    + 从本地推送分支至远程库
    + 推送失败，使用git pull 与远程库同步一下
    + 同步失败，git branch --set-upstream branch-name origin/branch-name，本地分支和远程分支的链接关系进行创建
- git checkout -b branch-name origin/branch-name
    + 在本地创建和远程分支对应的分支
- git branch --set-upstream branch-name origin/branch-name
    + 



