
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

### 将分支合并到当前分支
```
git merge 分支名
```

### 禁用fast-forward（快进），会多一个commit id
```
git merge --no-ff 分支名
```

### 回退到上一次提交（基于当前的commit）
```
git reset --hard HEAD^
```

### 回退到上上一次提交（都是基于当前的commit）
```
git reset --hard HEAD^^
```

### 回退到当前分支上的前n次（从当前commit往前n次）的提交
```
git reset --hard HEAD~n
```

### 回退到指定commit
```
git reset --hard commit信息的前几位
```

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
