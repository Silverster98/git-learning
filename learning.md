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


