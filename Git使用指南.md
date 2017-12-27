# Git使用指南

Git是一款免费、开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。

**安装好后首先git全局设置**：<br>
git config –global user.name “xxx”<br>
git config –global user.email “xxx@xxx.xxx”<br>
<br>
**新建git版本库并初始化**：<br>
mkdir test斜体文本<br>
cd test<br>
git init<br>
<br>
**添加文件到版本库**（提前创建好readme.txt）：<br>
git add readme.txt #添加文件<br>
git commit -m ‘<description>’ #提交文件 -m后面为文件描述<br>
<br>
> git可以多次add文件,但是只需要commit一次就好

git status 查看工作区状态<br>
git diff file #修改后文件与之前提交的文件内容对比<br>

git log #查看没有提交的描述<br>
git log –pretty=oneline #简化输出<br>
<br>
git reset –hard HEAD^ #回退到上个版本<br>
git reset –hard <id> #回到最新版本,id为commit id<br>
> 因为基于指针指向,所以git版本回退或者回到最新很快

git reflog #用来记录每一次命令,例如第二天想返回到最新版本可用此命令查看提交的id,再使用git reset –hard id返回即可<br>

**撤销修改**：<br>
1.修改后文件未使用git add添加文件<br>
git checkout — file #丢弃工作区修改<br>
2.修改后文件已使用add提交<br>
git reset HEAD file #撤销缓存区修改回到工作区<br>
git checkout — file #丢弃工作区修改<br>
<br>
**删除文件**：<br>
现有文件aaa,已add和commit<br>
1.确定删除<br>
rm -rf aaa #本地删除<br>
git rm aaa #git版本库删除<br>
git commit -m ‘<description>’ #commit修改<br>
2.误删除<br>
rm -rf aaa #本地删除<br>
git checkout — aaa #丢弃工作区修改<br>
<br>
**连接远程仓库**：<br>
先生成密钥文件(ssh-keygen -t rsa),将id_rsa.pub文件内容复制到远程仓库的ssh key页面内。<br>
在git上新建项目，根据新建完项目的提示来连接到远程仓库。<br>
git remote add origin git@172.16.4.112:pangc/test.git<br> #172.16.4.116(git地址),pangc(git用户名),test(项目名)<br>
git push -u origin master<br

> 由于远程库是空的，我们第一次推送master分支时，加上了-u参数，git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来

git push origin master #推送到远程仓库<br>

**创建于合并分支**：<br>
git checkout -b dev #创建并切换到一个名为dev的分支,相当于执行git branch dev和git checkout dev<br>
git branch #查看当前分支<br>
git merge dev #dev分支修改好后在master分支使用命令将dev分支合并到master<br>
git branch -d dev #合并好后可以删除dev分支<br>
<br>
**Bug分支**：<br>
git stash #保存当前状态,此时查看文件的话为之前未修改状态<br>
git stash list #当修改完成提交后切换到之前分支用命令查看stash列表<br>
1.git stash apply stash@{0} #使用命令恢复工作区<br>
git stash drop stash@{0} #删除stash<br>
2.git stash pop #恢复工作区自动删除<br>
<br>
**分支删除**：<br>
git branch -d/D <name> #d删除,D强制删除<br>
<br>
推送分支(获取master略过)：<br>
git branch –set-upstream dev origin/dev #设置dev和origin/dev的链接<br>
git checkout -b dev origin/dev #创建远程origin的dev分支到本地<br>
git push origin dev #add,commit完成后push到dev分支(默认dev分支,)<br>

**创建标签**：<br>
git tag v<tagname> #最新commit位置创建标签<br>
git tag v<tagname> <id> #以前commit位置创建标签,id为commit提交后生成的id(git log –pretty=oneline –abbrev-commit查看)<br>
git tag -a v<tagname> -m <description> <id> #tag添加描述<br>
<br>
**操作标签**：<br>
git tag -d v<tagname> #删除标签<br>
git push origin v<tagname> #推送某个标签到远程<br>
git push origin –tags #一次性推送全部尚未推送到远程的本地标签<br>
git tag -d v<tagname> #本地删除标签，删除完了需要远程仓库删除<br>
git push origin :refs/tags/v<tagname> #远程仓库删除<br>



