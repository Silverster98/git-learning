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
