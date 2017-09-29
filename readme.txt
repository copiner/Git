工作区 --> 暂存区 --> 版本库 --> 远程库

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

版本库的修改日志
git log
git log --pretty=oneline

回退到上一个版本
git reset --hard HEAD^

回到之前某个版本
git reset --hard 3628164

Git提供了一个命令，用来记录你的每一次命令
git reflog

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
