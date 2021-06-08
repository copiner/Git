### 工作区 --> 暂存区 --> 版本库    ----> 远程库

文件夹就是一个工作区，工作区有一个隐藏目录.git，这是Git的版本库

创建版本库
git init

丢弃工作区的修改
git checkout -- readme.txt

把工作区文件添加到暂存区
git add readme.txt

把暂存区的修改回退到工作区
git reset HEAD readme.txt

把文件提交到版本库
git commit -m "add a readme.txt file"     git commit只负责把暂存区的修改提交


查看仓库当前的状态
git status

查看修改信息
git diff readme.txt

版本库的修改日志，
git log
git log --pretty=oneline

把工作区文件回退版本库的上一个版本
git reset --hard HEAD^


回到版本库之前某个版本
git reset --hard 3628164 (commit id)

#### 后悔
回退到了某个版本，后悔了，想恢复到某版本，
Git提供了一个命令`git reflog`，用来记录你的每一次命令，可以找到`id`。

git reset --hard 3f5f1308

#### 添加到远程库
git remote add origin  git@github.com:copiner.git (仓库地址)

`添加后，远程库的名字，远程主机名origin，这是Git默认的叫法`。
本地库的所有内容推送到远程库上

git push -u origin master

删除远程库中文件或文件夹

git rm readme.txt

git commit -m "remove readme.txt file"
git push origin master

git rm -r storage/

git commit -m "remove storage"
git push origin master


### push

```bash
git push <远程主机名> <本地分支名>:<远程分支名>
```

如果本地分支名与远程分支名相同，则可以省略冒号：
git push <远程主机名> <本地分支名>

示例：
```bash
git push origin master
# 相等于
git push origin master:master

git push origin dev
# 相等于
git push origin dev
```

如果本地版本与远程版本有差异，但又要强制推送可以使用 --force 参数:

git push --force origin master


删除远程仓库分支
git push origin --delete dev

### pull
git pull 命令用于从远程获取代码并合并本地的版本

```
git pull <远程主机名> <远程分支名>:<本地分支名>
```

如果远程分支是与当前分支合并，则冒号后面的部分可以省略
git pull origin master

事实上，git pull是相当于从远程仓库获取最新版本，然后再与本地分支merge

```bash
#将远程主机origin的master分支拉取过来，与本地的dev分支合并
git pull origin master:dev

#将远程主机origin的master分支拉取过来，与本地的master分支合并
git pull origin master

#将远程主机origin的dev分支拉取过来，与本地的dev分支合并
git pull origin dev
```

### fetch

```bash
git fetch <远程主机名> <分支名>
```

不指定分支名，则会将某个远程主机的更新全部取回本地

```bash
# 取回origin主机的master 分支
git fetch origin master


#将远程主机origin的master分支拉取过来，与本地的dev分支合并
git fetch origin master:dev
git merge dev

#取回更新后，会返回一个FETCH_HEAD ，指的是某个branch在服务器上的最新状态，我们可以在本地通过它查看刚取回的更新信息
git log -p FETCH_HEAD


git merge FETCH_HEAD    #将拉取下来的最新内容合并到当前所在的分支中
```


### branch

新建分支
git branch dev

切换分支
git checkout dev

新建并切换到新建的分支上
git checkout -b dev

查看当前分支
git branch

查看远程所有分支
git branch -r

查看本地和远程的所有分支
git branch -a

git merge dev

删除本地分支
git branch -d dev

删除远程仓库分支
git push origin -d dev

重命名本地分支
git branch -m <oldbranch> <newbranch>


### merge

#### merge
```bash
# 执行以下命令
# 实现切换到master分支，合并dev分支到当前分支，即master分支，并且会多一个merge commit日志
git checkout master  
git merge dev
```
#### squash merge
```bash
# 执行以下命令
# 实现切换到master分支，合并dev分支到当前分支，即master分支，
# 但是并不会提交，本地会显示有东西修改需要手动add，commit，
# 但是因为手动add, commit后在dev的所有修改记录的修改人都会变成你自己
git checkout master  
git merge --squash dev
```

#### rebase merge
由于squash merge会修改提交人，对于以后查询日志不方便。使用rebase merge可以避开这个问题
```bash
# 执行以下命令
# 当执行了git rebase -i master命令后会出现一个编辑命令页面,可查看各个命令帮助
git checkout dev
git rebase -i master
git checkout master
git merge dev

```

### 备注
```bash

-d
--delete

-D
--delete --force

-f
--force

-m
--move

-M
--move --force

-r
--remote

-a
--all
```

### Git查看某个文件修改记录

1. git log filename

查看提交记录



2. git log -p filename

可以显示每次提交的diff



3. 查看某次提交中的某个文件变化，可以直接加上fileName

git show c5e69804bbd9725b5dece57f8cbece4a96b9f80b filename

TODO

### 暂存

当单人维护多版本的分支开发中，不小心弄混了分支，将自己新的需求代码混淆到了其他的分支上。可以使用git 的本地暂存。
使用以下命令，暂存本地未提交的修改

将工作区的修改保存到一个特定的空间去，然后将工作区的修改撤销掉。
需要注意的是，只能保存git已经跟踪的文件，新建文件并且没有commit过的就无法保存了，
而 git stash 暂存起来的修改是可以应用到当前或者其他分支上面去的
```
git stash
```
然后，切换到其他分支，也就是你要将修改合并到的分支
```
git switch xxx
```
然后,使用以下命令，弹出暂存的修改
```
git stash pop
```

```
git stash drop 删除某条暂存
git stash apply 应用某条暂存到当前分支
git stash clear 清空所有的暂存条目
```

### 其他
git中的checkout命令承载了分支操作和文件恢复的部分功能，有点复杂，并且难以使用和学习，
社区解决将这两部分功能拆分开，在git 2.23.0中引入了两个新的命令switch和restore用来取代checkout

新的switch命令用来接替checkout的功能，但switch不能切换到commit id
```
git switch aaa # 切换到 aaa分支
git switch -c aaa # 创建aaa，然后切换到 aaa分支
```

原来git中文件恢复涉及到两个命令，一个是checkout，一个是reset，reset除了重置分支之外，还提供了恢复文件的能力
```
git checkout -- aaa # 从staged中恢复aaa到worktree
git reset -- aaa # 从repo中恢复aaa到staged
git checkout -- HEAD aaa # 从repo中恢复aaa到staged和worktree
git reset --hard -- aaa # 同上
```

新的restore命令专门用来恢复staged和worktree的文件
```
git restore --worktree aaa # 从staged中恢复aaa到worktree
git restore --staged aaa # 从repo中恢复aaa到staged
git restore --staged --worktree aaa # 从repo中恢复aaa到staged和worktree

git restore --source=<commit>  # 从指定commit中恢复aaa到worktree
```
