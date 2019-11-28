## <center>git 分享（一）</center>

![](http://www.leyar.me/images/bg2015120901.png)

本地仓库由git维护的三颗“树”组成，第一个是“工作目录”，它持有实际文件；第二个是“暂存区”，它类似于缓存区域，临时保存你的改动；最后是“HEAD”，它指向你最后一次提交的结果



使用git的每次提交，Git都会自动把它们串成一条时间线，这条时间线就是一个分支。如果没有新建分支，那么只有一条时间线，即只有一个分支，在Git里，这个分支叫主分支，即master分支。有一个HEAD指针指向当前分支（只有一个分支的情况下会指向master，而master是指向最新提交）。每个版本都会有自己的版本信息，如特有的版本号、版本名等。
![](https://i.ibb.co/km6c4GY/HEAD.png)

- git clone 将远程仓库下载到本地，创建一个远程仓库的克隆版本
- <u>`git fetch / pull 将远程分支代码拉取到本地`</u>
- git checkout 切换分支
- git add 将修改的文件放入暂存区域
- git commit 给暂存区域生成快照并提交到当前分支
- git push 提交当前分支修改
- <u>`git reset / revert 回滚操作`</u>
- <u>`git rebase / merge 分支合并`</u>

---

### ***git fetch / pull***
`git fetch 将远程分支的代码拉到本地，开发者需要自己检查决定是否合并到工作分支`

```
git fetch <远程仓库> <分支>

🌰 git fetch origin master

在拉取更新之后，使用
git log -p FETCH_HEAD
来查看更新信息，通过更新信息来判断远程和本地是否会产生冲突，以及是否将更新的信息合并到本地分支
```
<br>

`git pull 将远程仓库的最新代码拉取下来后直接合并`
```
git pull <远程仓库> <远程分支>:<本地分支>

🌰 git pull origin master:develop

git pull的过程其实也可以理解为是git fetch + git merge 
```
---

### ***git reset / revert***
`git reset 将HEAD指向的位置改变为之前存在的某个版本`

![](https://i.ibb.co/KDVkwZm/reset.png)

适用场景：如果想恢复到之前某个提交的版本并且之后的提交的版本都可以不要，就可以使用reset
```
git reset --soft
只移动当前HEAD指针，不会改变工作区和暂存区的内容

git reset --mixed
移动HEAD指针，改变暂存区内容，但不会改变工作区(默认参数)
 
git reset --hard
HEAD指针、工作区和暂存区全部改变

🌰  使用git add提交到暂存区，但还没有commit
    - 可以直接使用 git reset --hard 覆盖当前暂存区和工作区
    - 可以使用 git reset --mixed 覆盖暂存区内容，在使用 git checkout . 用暂存区内容覆盖工作区内容

🌰  已经git commit，但还没有push
    - 使用 git reset --hard origin/master 从远程仓库把代码取回来，然后覆盖本地仓库、暂存区和工作区
    - 使用 git reset --hard <上一次commit id> 进行覆盖本地仓库、暂存区、工作区

🌰  已经push
    - 使用 git reset --hard <commit id> 将内容完全覆盖掉
```
git reset 通过取消缓存或者取消一系列提交的操作会摒弃一些你当前工作目录上的更改

<br>

`git revert 通过进行覆盖版本的操作来达到撤销该版本的修改`

![](https://i.ibb.co/TWSSXRj/revert.png)

适用场景：如果我们想撤销之前的某一版本，但是又想保留该目标版本后面的版本，记录下这整个版本变动流程，就可以用这种方法

```
git revert HEAD
撤销前一次的commit 

git revert HEAD^n
撤销前n次的commit

git revert <commit id>
撤销指定版本
```
---

### ***git rebase / merge***
`git rebase 会取消分支中的每个提交并把它们临时存放，然后把当前分支更新到最新的master分支，最后再把所有提交应用到分支上`

```
使用rebase合并多个commit
git rebase -i <commit startId> <commit endId>

```
<br>

`git merge 将两个分支，合并提交为一个分支`




#### ***git同时连接gitlab和github***
---
