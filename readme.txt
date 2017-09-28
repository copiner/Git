创建版本库
git init

添加文件到仓库
git add .

git add readme.txt

git commit -m "add a readme.txt file"

本地文件夹就是一个工作区，工作区有一个隐藏目录.git，这个是Git的版本库。

查看仓库当前的状态
git status
查看文件readme.txt的修改状态
git diff readme.txt

查看历史记录
git log

git log --pretty=oneline

回退readme.txt到上一个版本
git reset --hard HEAD^


记录你的每一次命令
git reflog

丢弃工作区的修改
git checkout -- readme.txt

回退readme.txt到之前某个版本
git reset --hard 3628164


从版本库中删除某文件，那就用命令git rm删掉，并且git commit
git rm readme.txt
git commit -m "remove test.txt"


添加远程库
git remote add origin git@github.com:xxxxx/zzzzzz.git
添加后，远程库的名字就是origin

把本地库的所有内容推送到远程库
git push -u origin master


从远程库克隆
git clone git@github.com:xxxxx/zzzzzz.git

Git删除远程仓库中的文件
git rm readme.txt
git commit -m "remove readme.txt"
git push -u origin master
