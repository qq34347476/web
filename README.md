# git 安装配置

## 0. 安装 Git

网上有很多 Git 安装教程，如果需要图形界面，windows 下建议使用 TortoiseGit，linux 建议使用 Git GUI 或者 GITK。

## 1. Git 基本配置

git config 可以配置 git 的参数，可以使用 git config --list 查看已经配置的 git 参数。其中有三个级别的保存位置，

    --system、--global、--local，分别表示所有用户（本系统）、当前用户（全局）、本地配置（当前目录），默认使用--local。

### 配置用户名及邮箱

在使用 Git 提交前，必须配置用户名和邮箱，这些信息会永久保存到历史记录中。

    git config --global user.name "Tocy"
    git config --global user.email zyvj@qq.com

其他配置

    如果在windows下建议还是配置下默认文本编辑器core.editor和差异分析工具merge.tool。

## 2. 创建 Git 仓库

    可以直接调用git init初始化当前目录，即创建Git仓库。

## 3. 获得 Git 仓库

如果需要克隆远程仓库，可以使用 git clone，比如：

    git clone https://github.com/qq34347476/web.git

## 4. 提交更新

在 windows 下的 Git GUI 中，提交很简单，右键-TortoiseGit-Commit。那么命令行下需要怎么处理？

    Git中每个文件都有三种状态：committed、staged、modified。它们之间关系如下：
        commit <-- stage <-- modify
        commit --> --- --modify

我们获取的 Git 仓库中的所有文件都是 committed 状态，

如果你在本地修改了文件 a，a 的状态就变成 modified 的；

如果使用 git add a，a 的状态变成 staged；

如果使用 git commit，a 的状态就变成 commited。

这种状态变化也说明复制代码是很方便的，但是提交更新请慎重。

当然还有一种文件状态，未跟踪状态（unversioned/untracked），通过使用 git add 可以把未跟踪状态变更为 staged；通过 git rm 可以将 staged 或者 committed 状态变为未跟踪状态。

### git status

通常提交前先检查下修改了什么内容，当前 Git 目录下各文件的状态。

    $ git status
    On branch master

    Initial commit

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

    nothing added to commit but untracked files present (use "git add" to track)

### git add

git add 可以添加文件或者目录，也可以使用通配符。比如：

    git add Readme.md    # add file only
    git add *.cpp        # add all cpp files
    git add /home/code/  # add all files in /home/code
    git diff
    git diff可以查看当前目录的所有修改。

提交之前，还是单独确认下处于 staged 状态的文件有哪些，并保证修改正确。在实际应用中，可能还需要使用 git diff 导出 PATCH 做代码走读。

可以使用 git diff --staged 或 git diff --cached 查看 staged 与上次提交快照之间的区别。

### git commit

提交前需慎重。直接调用 git commit 会弹出编辑器，输入提交日志（如果是多行日志，建议使用）。

    针对单行日志提交的情况，可以使用如下命令：
        git commit -m "add readme"。
    还有一种快捷的提交方式，直接跳过stage缓存区，直接提交当前目录下的所有修改
        git commit -a（使用这个命令前建议确认下当前目录的修改是否正确、必须）。

### git rm

git rm 会把文件从当前目录删除（不会保存删除的文件）。
如果需要从 Git 仓库中删除，但保留在当前工作目录中，亦即从跟踪清单中删除，可以使用

    git rm --cached readme.md。

## 5. 提交历史查看

可以使用 git log 查看当前工程的所有提交的日志。

    git log --stat      # 仅显示摘要选项
    git log --pretty=oneline        # 定制记录格式
    git log --graph     # 图像化分支和版本更新

## 6. 撤销更新

## 7. 远程仓库

可以使用 git remote 查看当前的远程库。

### git remote -v 可以显示对应的克隆地址。（对于多个远程仓库很有用）

### 添加远程仓库

    git remote add [short_name] [url]可以添加新的远程仓库。

### 从远程仓库抓取数据

    git fetch [remote-name]可以从远程仓库抓取数据到本地。
    也可以使用git pull

### 推送数据到远程仓库

    git push [remote_name] [branch_name]
    默认使用origin和master。

### 查看远程仓库信息

    git remote show origin

### 远程仓库的删除和重命名

    git remote rename [old_name] [new_name]
    git remote rm [remote_name]

## 8. 打 Tags

可使用 git tag 显示当前库中的标签。

添加标签（含附注）

    git tag -a v0.1 -m "my version 0.1"
        使用如下命令查看Tag日志信息（指定对应标签的名字）
            git show v0.1
        也可使用SHA-1的提交表示创建tag：
            git tag -a v0.2 [SHA-1] -m "my version 0.2"

分享标签

    默认的，git push不会推送标签信息到远程仓库，需要通过命令显式推送。
        git push origin v0.1
    如果需要推送所有标签，使用
        git push origin --tags

## 9. Git 分支

git 分支是轻量级的，速度很快，仅记录索引信息。

### 显示所有分支

    使用git branch可显示当前所有分支。
    可以使用--merged和--no-merged查看已经合并、未合并的分支。

### 创建及切换分支

可以使用下面命令直接切换并创建分支

    git checkout -b testing

等价于

    $git branch testing    # 创建testing 分支
    $git checkout testing  # 切换到testing分支

注意切换分支时请保持工作目录没有未提交的修改。Git 鼓励使用分支，处理完问题之后合并分支即可。

### 分支合并

将 hotfix 分支合并到 master（主分支）上，需要通过下面命令：

    $git checkout master
    $git merge hotfix

合并之后可以使用 git branch -d hotfix 删除分支。
如果合并时存在冲突，需要手工修改。
