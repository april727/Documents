# The step  of git 
-------------------------
# 准备

1. git init  #本地库初始化
2. git remote add origin <ssh协议地址(免密)> #远端库别名origin 
	1. ssh协议格式： git@github.com:april727/documents.git 
	2. git remote 或者 git remote -v 查看远端库的别名
3. git status #查看本地库状态
--- 
# 添加

1. git add #添加本地库所有文件到暂存区
2. git commit #添加所有暂存区文件到本地库
3. git commit -m "Added GIT-A.md file to git directory." #新的文件或者修改后的文件
4. git push origin main #推送本地库内容到远端库origin的main分支
5. git pull origin main #拉去远端库所有内容到本地库，并且合并merge
	-  git fetch origin main #拉去远端库所有内容到本地库，但是不合并merge
6. git remote show origin #查看远端代码库信息
---
# 分支

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
---
