### 工作区 --> 暂存区 --> 版本库 --> 远程库

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
git commit -m "add a readme.txt file"  git commit只负责把暂存区的修改提交

仓库当前的状态
git status

查看修改信息
git diff readme.txt

版本回退

回退到上一个版本
git reset --hard HEAD^

版本库的修改日志，
git log
git log --pretty=oneline

回退到上一个版本
git reset --hard HEAD^

回到之前某个版本
git reset --hard 3628164

再回到之前版本,找到之前commit id,就可以了
git reset --hard 3f7f1308

另外：
回退到了某个版本，后悔了，想恢复到某版本，
Git提供了一个命令，用来记录你的每一次命令，可以找到commit id。
git reflog

git reset --hard 3f5f1308

添加到远程库
git remote add origin git@github.com:yyyyyyyyy/xxxxx.git

添加后，远程库的名字就是origin，这是Git默认的叫法。
本地库的所有内容推送到远程库上
git push -u origin master

删除远程库中文件
git rm readme.txt
git rm -r storage/

git commit -m "remove readme.txt file"
git push origin master


### 远程主机名 即  origin

### push

```bash
git push <远程主机名> <本地分支名>:<远程分支名>
```
如果本地分支名与远程分支名相同，则可以省略冒号：
git push <远程主机名> <本地分支名>

示例
```bash
git push origin master
# 相等于
git push origin master:master
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

git pull是拉取远程分支更新到本地仓库的操作。
比如远程仓库里的学习资料有了新内容，需要把新内容下载下来的时候，就可以使用git pull命令。
事实上，git pull是相当于从远程仓库获取最新版本，然后再与本地分支merge（合并）

```bash
#将远程主机origin的master分支拉取过来，与本地的dev分支合并
git pull origin master:dev
```


### fetch
git fetch不会进行合并，执行后需要手动执行git merge合并，而git pull拉取远程分之后直接与本地分支进行合并

```bash
git fetch <远程主机名> <分支名>
```

```bash

git fetch origin master

#取回更新后，会返回一个FETCH_HEAD ，指的是某个branch在服务器上的最新状态，我们可以在本地通过它查看刚取回的更新信息
git log -p FETCH_HEAD


git merge FETCH_HEAD    #将拉取下来的最新内容合并到当前所在的分支中
```



git fetch更新本地仓库的两种用法

```bash
# 方法一
#将远程主机origin的master分支拉取过来，与本地的dev分支合并
git fetch origin master:dev
git merge dev
```

```bash
$ git fetch origin master                #从远程的origin仓库的master分支下载代码到本地的origin maste
$ git log -p master.. origin/master      #比较本地的仓库和远程参考的区别
$ git merge origin/master                #把远程下载下来的代码合并到本地仓库，远程的和本地的合并
```

```bash
# 方法二
$ git fetch origin master:temp           #从远程的origin仓库的master分支下载到本地并新建一个分支temp
$ git diff temp                          #比较master分支和temp分支的不同
$ git merge temp                         #合并temp分支到master分支
$ git branch -d temp                     #删除temp
```

### merge

```bash
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

查看所有分支
git branch -a

git merge dev

删除分支
git branch -d dev

删除远程仓库分支
git push origin --delete dev
