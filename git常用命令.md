
## 分支

### 查看分支

```
git branch
```

### 创建分支

```
git branch 分支名
```

### 切换分支

```
git checkout 分支名
```

### 切换到上次处于的分支中
```
git checkout -
```

### 删除分支
```
git branch -d 分支名
```
> 注意：这里需要注意不能删除当前处于的分支，如果非master分支有改动但还未merge的话也不可以，除非使用git branch -D 分支名

### 创建新分支并切换到新分支
```
git checkout -b 分支名
```

### 显示当前分支最近的一条提交消息
```
git branch -v
```

### 分支合并
  注意：`--no-ff`是不快速合并的意思

* git merge 与git merge --no-ff的区别？

  已`master`合并`release`分支为例，合并release后，merge形式的合并在master上会作为一个commit（即与master一条线）
  
  ![merge1](./file/merge1)
  
  但是`--no-ff`形式的合并在master上不会作为一个commit（即不与master一条线），但会产生新的合并点。
  
  ![mergeNoFF](./file/mergeNoFF)

### 将分支合并到当前分支
```
git merge 分支名
```

### 禁用fast-forward（快进），会多一个commit id
```
git merge --no-ff 分支名
```

### 回滚提交
在需要回滚一次或多次提交时可以用这个命令。由于该命令比较危险，建议用于已经把最新提交推送到远程仓库

* git reset HEAD [filename] 

> 把已在暂时区的文件取消，恢复到已修改未暂存状态。
  
* git reset HEAD~[n]

> 表示回退到n个提交之前。同时，它也可以用来合并提交。下面的写法与git commit --amend结果是一样的。
  
  ```
  git reset HEAD~2
  git commit
  ```

* 三种参数
> git reset --hard [commitID]，改引用，改暂存区，改工作区与引用指向的目录一致。    
> git reset --soft [commitID]，只更改引用的指向，不改变暂存区和工作区。       
> git reset --mixed [commitID]或git reset [commitID](默认)，更改引用的指向及重置暂存区，但是不改变工作区       

### 修改分支名
```
git branch -m 原分支名 新分支名
```

### 将工作区的修改保存
```
git stash list
```

### 列出所有的保存
```
git stash list
```

### 手动设置stash描述
```
git stash save 'hello basic'
```

### 恢复最近一次的保存，并且会把这次保存在列表中删除
```
git stash pop
```

### 恢复最近一次的保存，但是不会在列表中删除
```
git stash apply
```

### apply特定一个版，并且会把这次保存在列表中删除
```
git stash apply stash@{0}
```

### 手动删除指定的一个保存版本
```
git stash drop stash@{0}
```

### 创建轻量标签
```
git tag v1.0.1
```

### 创建附注标签
```
git tag -a v1.0.2 -m 'release 1.0.2'
```

### 查看所有标签
```
git tag
```

### 查找标签
```
git tag -l 'v1.0' 里面可以使用pattern，例如'v*', 代表v开头的所有标签
```

### 删除标签
```
git tag -d 标签名
```

### 列出每一行都是谁在什么时间哪个commit修改的
```
git blame 文件名
```

### 比较算入暂存区修改的当前文件与工作区文件之间的区别
```
git diff
```

### 比较当前最新commit与工作区的区别
```
git diff HEAD
```

### 比较某个commit与工作区的区别
```
git diff commit_id
```

### 比较最新提交与暂存区的区别
```
git diff --cached
```

### 比较某个commit与暂存区的区别
```
git diff --cached commit_id
```

### 查看commit日志
```
git reflog：
  d171231 HEAD@{0}: commit: <E4><BF><AE><E6><94><B9><E6><A0><B7><E5><BC><8F><E7><9A><84><E4><B8><9C><E8><A5><BF>
  a254958 HEAD@{1}: checkout: moving from dev to pmDetail
  232eace HEAD@{2}: pull zaihui dev: Fast-forward
  19cd548 HEAD@{3}: checkout: moving from pmDetail to dev
  a254958 HEAD@{4}: commit: tmp
  e71c811 HEAD@{5}: checkout: moving from pmDetail to pmDetail
git log：
  commit d1712318017337897d232b2e73be8a9d3e0c7470
  Author: dingyanhe <dingyanhe@kezaihui.com>
  Date:   Thu Apr 12 11:06:37 2018 +0800

      <E4><BF><AE><E6><94><B9><E6><A0><B7><E5><BC><8F><E7><9A><84><E4><B8><9C><E8><A5><BF>

  commit a254958ae6809d7538bea4ff4e234daff96c84c4
  Author: dingyanhe <dingyanhe@kezaihui.com>
  Date:   Wed Apr 11 15:01:45 2018 +0800

      tmp

```

### 覆盖commit日志，合并提交
```
git commit --amend
```
最常见的用法是上次提交信息写错了，或者提交多了或者漏了，重新提交覆盖上一次提交。
其实他还有一个用法，就是用来合并提交。例如上次提交的修改并不完全，再作修改之后就可以用该名命令把上次提交合并在一起。‘

