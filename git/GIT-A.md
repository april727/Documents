# 🏠The step  of git 
-------------------------
## 准备

1. git init  #本地库初始化
2. git remote add origin <ssh协议地址(免密)> #远端库别名origin 
	1. ssh协议格式： git@github.com:april727/documents.git 
	2. git remote 或者 git remote -v 查看远端库的别名
3. git status #查看本地库状态
	**其他查看信息命令**
	- git status -s or git status --short 
	- git diff
	
--- 
## 添加

1. git add "具体文件名" #添加本地库所有文件到暂存区
	- git add . #添加当前目录下所有文件：新添加的，修改后的，不包括删除的文件到暂存区
	- git add * #添加当前目录下所有文件：新添加，修改过，删除的的文件到暂存区
	- git reset HEAD CONTRIBUTING.md #取消暂存区的CONTRIBUTING文件
1. git commit #添加暂存区文件到本地库
	- 首先通过git status 查看暂存区时候有文件(绿色)
	- git commit -m “commit message” #添加所有暂存区的内容到本地库
	- git commit -a -m “commit message” #添加所有被add跟踪文件到本地库，包括add后文件再被修改的也会被直接提交到本地库，如果不使用这个-a参数，这样被修改后的文件需要重新add到暂存区，才能commit；而使用了-a这个参数，被修改后的文件可以不需要add直接添加到本地库；
	- git commit  "file name"  #这个命令将进入文本编辑器，需要在文本编辑器中添加"commit message"
		- 举例：git commit -m "Added GIT-A.md file to git directory." #新的文件或者修改后的文件，其中引号的内容是对这个推送的描述 
	- git commit --amend #修改上次提交的信息
		### 完整的步骤
			1. git commit -m "修改后的commit message"
			2. git push -f origin main # 提交修改后的信息到远端的origin库的main分支
2. git log #查看提交的历史记录
	1. git log --pretty=format:"%h %s" --graph
	2. -p -2or --patch -2 #显示的提交数量
	3. --stat #显示每次提交的变化
3. git push origin main #推送本地库内容到远端库origin的main分支
4. git pull origin main #拉去远端库所有内容到本地库，并且合并merge
	-  git fetch origin main #拉去远端库所有内容到本地库，但是不合并merge
---
## 分支

1. 分支
	 - 创建分支：git branch new_branch
	 - 切换分支：git checkout new_branch
	 - 合并分支：
		 1. git checkout main #切换到主分支
		 2. git merge new_branch #new_branch分支合并到main主分支上
		 3. git branch -d new_branch #删除合并后不需要的new_branch
		 4. merge 和 rebase 区别，变基使分支更加整洁，同时丢失了历史记录信息
	- 分支管理
		 1. git branch #显示所有分支 
		 2. git branch -v #查看每个分支最后的提交
		 3. git branch --merge #查看已经合并的分支
		 4. git branch --no-merged #查看未合并的分支
2. 跟踪分支(本地跟踪一个远端库的分支)
	- git checkout -b serverfix origin/serverfix
	- git checkout --track origin/master
	- git checkout -b sf origin/serverfix #这表示本地分支跟踪的远端库分支具有不同的名字，本地分支重新起名为sf
	- git branch -u origin/serverfix #修改正在跟踪的上游分支
	- git branch -vv #查看所有的本地分支跟踪的上游分支
	- git fetch --all; git branch -vv #这个和上一个命令不同在于，这会显示你本地每个分支和远端库最新分支的差距，而上一个显示的是本地分支和你最后一次抓取的数据差异
1. 推送本地分支到远程库
	- git push orgin serverfix #推送本地库serverfix到远程库的serverfix分支
	- git push orgin serverfix：awesomebranch #推送本地库serverfix到远端库，并将这个分支在远端库命名为awesomebranch	
	- git remote show origin #查看远端代码库信息
---
## 打标签
1. 列标签
	 - git tag 
	 - git tag -l "v1.8.5*" #这里使用正则显示标签
 2. 创建标签
	 1. 创建附注标签：git tag -a v1.0 -m "my version 1.0"
	 2. 创建轻量标签：git tag -v1.0 
 3. 显示某一标签信息：git show V1.0
 4. 后期标签
	 1. git log --pretty=oneline #显示所有的提交点信息
	 2. git tag -a v1.1 9fceb02 #后边的代码表示对应提交信息的哈希值
5. 传送标签到远端库
	- git push origin v1.1 #推送一个具体的标签
	- git push prigin --tags #推送多个本地标签到远端库
6. 删除标签
	- 删除本地库标签：git tag -d v1.1
	- 删除远端库标签：在删除本地库标签后，git push origin ：refs/tags/v1.1 或者 git push origin --delete v1.1
7. 检出标签(查看某一具体的文件版本)
	- git checkout v1.1
	- 此刻你处于分离头状态(detached HEAD)，在这时你提交了一些变化，标签不会发生变化，但是你的提交分支，无法访问，除非使用具体的哈希值才能访问，因此如果你需要对某个特定的版本进行修改的时候需要创建分支：git checkout -b version2 v1.1；如果这时你在提交，