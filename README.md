# -web
移动web基础
============================================
Git 工具总结

初操作---设置用户名
git config --global user.name "any name"  //设置全局project的用户名
git config --global user.email "any email"  //设置全局project的邮箱
git config --global --list   //查看当前用户的全局配置   用户名和邮箱
在VS Code中每次更新代码都会要输入账号密码，方便起见，可以配置一下让 git 记住密码账号。
git config --global credential.helper store 
 

 建立远程仓库链接
如果是从服务器 clone 下来的代码，会自动配置一个叫 origin 的远程仓库链接
git remote -v  // 查看配置的远程仓库链接
git remote add <远程仓库名> <远程仓库url>    //添加远程库链接
git remote rm <远程仓库名>   //移除远程仓库
git remote rename <oldname> <new name> //远程仓库重命名
 

 提交代码过程
提交之前，需要 pull 一下，然后处理冲突
git add -A   //添加所有文件，也可以只提交更改的文件 git add .
git add .   //添加更改的文件
git commit -m "描述代码信息"
git push -u <远程库的名称> <远程库的分支>  // -u 表示指定<当前远程库> 为默认远程仓库，以后就直接push，不用带参数
如果你确定远程仓库的分支上那些代码都不需要了，那么直接 push 后面加一个 -f ，强行让本地分支覆盖远程分支
git push <远程仓库名> <远程库的分支> -f 
 

提交代码出现冲突
git push 会出问题，应该先pull 一下，但是 pull 的时候又可能会出现分支冲突，
这时可能由于版本问题会报错，可能遇到 refusing to merge unrelated histories 这个提示是因为两个仓库不同，发现 refusing to merge unrelated histories，无法 pull。
要把两个不同的项目合并，git 需要添加一句代码 ，这句代码是在 git 2.9.2 版本发生的，最新的版本需要添加 –allow-unrelated-histories。查看git 版本，git --version
假如我们的远程仓库是 origin，分支是 master，那么我们 需要这样写  git pull origin master --allow-unrelated-histories
然后再  git push -u <远程库的名称> <远程库的分支>
 

拉取代码出现冲突
git pull 时本地文件和远程服务器文件冲突，出错信息如下：
error: Your local changes to 'contextTempl.java' would be overwritten by merge.  Aborting.
Please, commit your changes or stash them before you can merge.
解释：这个意思是说更新下来的内容和本地修改的内容有冲突，先提交你的改变或者先将本地修改暂时存储起来。
在 VS Code 中，错误提示是：在签出前 请清理存储库工作树
在这种情况下，您可以将更改隐藏起来，然后执行git pull，然后解压缩；
git stash  //先将本地修改存储起来
git pull  //拉取远程
git stash pop //还原暂存内容
 

代码克隆所有分支
　　git clone 只能 clone 远程库的 master 分支，无法 clone 所有分支，解决方法去下：

git clone http://xxx.xxx.com/project/.git ,这样在git_work目录下得到一个project子目录
cd project
git branch -a，列出所有分支名称如下：remotes/origin/dev     remotes/origin/release
git checkout -b origin/dev dev，作用是 checkout 远程的 dev 分支，在本地起名为 dev 分支，并切换到本地的 dev 分支
git checkout -b origin/release release，作用参见上一步解释
git checkout dev，切换回 dev 分支，并开始开发。
 

　　查看分支：git branch

　　创建分支：git branch <name>

　　切换分支：git checkout <name>

　　创建+切换分支：git checkout -b <name>

　　合并某分支到当前分支：git merge <name>

　　删除分支：git branch -d <name>

 

指令简写
　　-d    --delete：删除

　　-D   --delete --force的快捷键

　　-f     --force：强制

　　-m   --move：移动或重命名

　　-M   --move --force的快捷键

　　-r     --remote：远程

　　-a     --all：所有

 

git fetch 和 git pull 的区别
git fetch <远程主机名> <分支名>
最常见的命令如取回 origin 主机的 master 分支：
git fetch origin master  ，从远程主机的master分支拉取最新内容
git merge FETCH_HEAD ， 将拉取下来的最新内容合并到当前所在的分支中
git pull <远程主机名> <远程分支名>:<本地分支名>
git pull origin master  ， 如果远程分支是与当前分支合并，则冒号后面的部分可以省略
 

git 撤销操作、恢复文件
如果误删了某文件，需要 git status 先看下工作区是否 commit 过，如果没有 commit ，可以看到删除的文件名及路径，是红色的
直接从工作区拿删除的文件 git checkout -- <path + file>
如果已经commit 了，那么git status 看到的删除的文件及路径是绿色的，这时checkout 已经没用了
可以把暂存区的修改撤销掉（unstage），git reset HEAD <path + file>，重新放回工作区，然后 git checkout -- <path + file> 取回
 

git 版本回退
远程分支回退有三种方法：

自己的分支回滚直接用 reset
公共分支回滚用 revert
错的太远了直接将代码全部删掉，用正确代码替代
本地分支版本回退：

先找到要回退的版本的 commit id ，git reflog 
可以根据commit id ，查看先前版本的信息，git log <commit id>  或者 git show <commit id>，退出git log 状态，英文状态下按q 
回退版本 git reset --hard <commit id> 
自己的远程分支版本退回：

　　如果你的错误提交已经推送到自己的远程分支了，那么就需要回滚远程分支了。

git reflog
git reset --hard <commit id>
然后强制推送到远程分支，git push -f
本地分支回滚后，版本将落后远程分支，必须使用强制推送覆盖远程分支，否则无法推送到远程分支
公共远程分支回退：

　　回滚公共远程分支和回滚自己的远程分支是有区别的，如果你回退公共远程分支，把别人的提交给丢掉了怎么办？