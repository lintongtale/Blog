---
title: Git教程
date: 2017-06-03 18:48:04
commets: true
tags:
- git
- 教程
categories:
- 编程
- git
description:
- Git教程。
---
## Git安装
* <code> git config --global user.name "Your name" </code>
* <code> git config --global user.email "Your email" </code>
	注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址


## 远程仓库
* <code> ssh-keygen -t rsa -C "youremail@example.com" </code>
	在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥
* <code> git remote add origin git@github.com:lintongtale/test.git </code> 将本地仓库与远程仓库关联
* <code> git push -u origin master </code> 把当前分支推送到远程，-u把本地分支和远程分支关联起来，在以后的推送或拉取时可以简化命令  
	<code> git push origin master </code>
* <code> git clone git@github.com:lintongtale/test.git </code> 从远程克隆一个本地库  
	<code> ls </code> 列出所有文件


## 版本控制
![git状态转移](http://wx2.sinaimg.cn/mw690/c2781ec1ly1fgdvkucbtkj20do07pdgr.jpg)
* <code> mkdir \file.txt </code> 创建一个空目录  
	<code> cd \file.txt </code>  
	<code> pwd </code>
* <code> git init </code> 把当前目录变成Git可以管理的仓库
* <code> git add file.txt </code> 添加到暂存区  
	<code> git add . </code> 将内容修改和新文件添加到暂存区，不包括删除的文件  
	<code> git add -u </code> 更新已经被add的文件，不提交新文件（untracked file）  
	<code> git add -A </code> 上面两个功能的合集
* <code> git commit -m </code> "说明"
* <code> git log </code> 显示从最近的提交日志<code>git log --pretty=oneline
	pretty </code> 按指定格式显示日志信息,可选项有：oneline,short,medium,full,fuller,email,raw以及format
* <code> git reset --hard HEAD^ </code> 回退到上一个版本  
	<code> git  reset --hard HEAD^^ </code> 回退到上上一个版本  
	<code> git reset --hard HEAD~100 </code> 往上100个版本  
	<code> git reflog </code> 记录每一次命令，包括commit id  
	<code> git reset --hard <commit id> </code>
* <code> git status </code> 查看状态
* <code> git diff HEAD -- file.txt </code> 查看工作区和版本库里面最新版本的区别
* <code> git checkout -- file.txt </code> 让文件回到最近一次git commit或git add时的状态（撤销修改）
	* <code> git checkout -- file.txt </code> 取消某个文件修改
	* <code> git checkout . </code> 取消所有文件修改
* <code> rm file.txt </code> 删除文件  
	<code> git rm file.txt </code>  
	<code> git commit -m "remove file" </code>  
	若发现删错了，<code> git checkout -- file.txt </code>


## 分支管理
* <code> git checkout -b test </code> 创建test分支，并切换到test分支，-b表示创建并切换，相当于以下两条命令  
	<code> git branch test </code> 创建分支  
	<code> git checkout test </code> 切换分支  
	<code> git branch </code> 查看当前分支
* <code> git merge test </code> 将test分支合并到master分支上，Fast forward模式，<删除分支时会丢失分支信息>
	* <code> git merge --no-ff -m "merge with no-ff" </code> 合并分支，no-ff表示禁用Fast forward，<删除分支时不会丢失分支信息>
* <code> git branch -d test </code> 删除test分支
* <code> git log --graph </code> 查看分支合并图  
	当master分支和test分支各自都有新的提交时，Git无法快速合并，只能试图将各自的修改合并起来。
* <code> git branch -a </code> 查看远程分支

### Bug分支
* 当你在dev分支上进行的工作还没有提交，而此时有一个代号为101的bug任务，需要另外临时创建一个issue-101来修复它  
	git stash 把当前工作现场“储藏”起来，等以后恢复现场后继续工作，此时git status工作区是干净的  
	假设需要在master分支上修复bug，创建临时分支issue-101修改并merge后  
* <code> git stash list </code> 查看刚才的工作现场
	<code> git stash apply </code> 恢复
	<code> git stash drop </code> 删除stash内容
	<code> git stash pop </code> 等同于前两步

### Feature分支
* 软件开发中，每添加一个功能时，应该创建一个feature分支，完成后再合并。
* 当分支完成并commit后，如果此时功能需要取消，要删除feature分支，此时，使用<code> git branch –d feature-vulcan </code>将会出现error
* <code> git branch –D feature-vulcan </code> 强行删除feature-vulcan分支

### 多人协作
* <code> git remote –v </code> 查看远程仓库的信息
* <code> git push origin master </code> 推送分支，<code> git push origin dev </code>推送dev分支
* master是主分支，要时刻与远程同步；dev是开发分支，团队所有成员都需要在上面工作，需要远程同步；bug分支只用于本地修复bug，无需推送到远程；feature分支是否推送到远程，取决于你是否和其他人合作在上面开发
* <code> git checkout –b dev origin/dev </code> 创建远程origin的dev分支到本地。此时，可以在dev分支上修改，并push到远程；若此时，另一个人同样在对dev分支的文件作了修改，并试图推送，出现erro并提示“current branch is behind”
* <code> git pull </code> 把最新的提交从远程抓下来  
	* 相当于从远程获取最新版本，并merge到本地，更安全的做法是：  
	<code> git fetch origin master </code>  
	<code> git log -p master..origin/master </code>  
	<code> git merge origin/master </code>
* <code> git branch –set-upstream dev origin/dev </code> 指定本地分支dev与远程origin/dev分支链接，之后才能git pull。此时，将本地修改与远程merge，但是会有冲突，需要手动解决，解决后commit再push


## 标签管理
* <code> git tag v1.0 </code> 创建标签；默认标签是打在最新提交的commit上的
* <code> git tag </code> 查看所有标签
* <code> git log –pretty=oneline –-abbrev-commit </code> 查找到相应的commit id例如6224937；然后打标签
* <code> git tag v0.9 6224937 </code>
* <code> git tag –a v0.1 -m "version 0.1 released" 3628164 </code> 创建带有说明的标签，-a指定标签名，-m指定说明文字
* <code> git tag –s v0.2 -m "signed version 0.2 released" </code> 用PGP签名标签
* <code> git tag –d v0.1 </code> 删除标签
* <code> git push origin v0.1 </code> 推送标签到远程
* <code> git push origin –tags </code> 一次性推送全部尚未推送到远程的本地标签
* <code> git push origin :refs/tags/v0.9 </code> 删除远程标签，需先删除本地标签


## 自定义Git
* <code> touch .gitignore </code> 添加.gitignore文件
* <code> git check-ignore –v App.class </code> 检查.gitignore的规则错误
* <code> git config –global alias.st status </code> 配置status的别名，此时git st等效于git status
* <code> git config –global alias.unstage 'reset HEAD' </code> 此时git unstage test.py相当于git reset HEAD test.py，即把暂存区的修改撤销掉（unstage）
* <code> git config –global alias.last 'log -1' </code> 此时，用git last就能显示最近一次的提交
* <code> git config –global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'  --abbrev-commit" </code>


## git 命令
* <code> git add . </code> 同时添加多个已修改的文件到暂存区。
* <code> q </code> 退出

撤销修改

查看之前的commit
* <code> git checkout <commit> file.txt </code>
* <code> git checkout &lt commit &gt </code>
* <code> git checkout <branch> </code>

撤销公共修改
* <code> git revert <commit> </code>

撤销本地修改
* <code> git reset </code>
* <code> git clean </code>

重写Git历史记录
* <code> git commit –amend </code>
* <code> git rebase </code>
* <code> git reflog </code>

git bash 出现vim的时候如何退出
* 一直按住Esc，再连续按大写的z两次

<code> cd .. </code> 返回上一级目录  
<code> cd file.txt </code> 进入某一目录


## git submodule子模块
添加
* <code> git submodule add </code> 仓库地址 路径  
	注意：路径不能以 / 结尾（会造成修改不生效）、不能是现有工程已有的目录。

删除
* 首先，要在“.gitmodules”文件中删除相应配置信息。然后，执行<code> git rm –cached </code>命令将子模块所在的文件从git中删除。

下载的工程带有submodule
* 当使用git clone下来的工程中带有submodule时，初始的时候，submodule的内容并不会自动下载下来的，此时，只需执行如下命令：  
<code> git submodule update --init --recursive </code>
即可将子模块内容下载下来后工程才不会缺少相应的文件。


## 常见问题
* merge 冲突，git界面显示“# Please enter a commit message to explain why this merge is necessary”，按照下列步骤解决：
	* Press i to enter insert mode.
	* Now you can type your message, as if you were in a normal (non-modal) text editor.
	* Press esc to go back to command mode.
	* Then type :w followed by enter to save.
	* Finally :q followed by enter to quit.
	* 另：一直按住Esc，再连续按大写的z两次

* 本地克隆远端非Master分支
	* <code> cd RepoPath </code>
	* <code> git branch </code>
	* <code> git checkout -b branchName origin/branchName </code>
