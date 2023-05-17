# git


![[Pasted image 20230511113113.png]]
 
---
## 状态

- 跟踪和未跟踪
- add的三种用途
- 三个空间和四种状态
--- 
## 基础
- status
	▪ git status
	▪ git status -s # --short
	▪ ![[Pasted image 20230511113346.png]]
	??未跟踪；A暂存区；M修改过；双栏：左暂存，右工作；
	▪ git diff➤一种更加清晰文件变化的信息查看
- .ignore➤去除不可被跟踪文件：敏感文件或者无用的文件
	▪ 正则表达式可用来选则文件
- commit➤stage中的文件，提交到repository中
	1. 编辑器查看文档内容
		编辑器：vim，emacs
	2. 跳过暂存直接commit
		git commit -a # 将所有跟踪过的文件暂存起来，一并提交，绕过git add步骤
		🌟这个命令需要小心：其会将所有modified过后的文件，有可能会将不需要的文件commit；
- 移除文件
	1. rm 工程名➤从工作区(本地工程文档)移除
	2. git rm 工程名➤
		1. 如果文件只是add到暂存区而没有commit，跟踪文件中删除，或者说从暂存区删除➤未跟踪文件
		2.  如果文件已经commit➤这文件在staging中状态是deletion，下次commit时，在repository和working中都删除；如果你后悔了，改变想改变文件在staging中的deletion状态，使用git reset README.txt, 这样消除文件在staging中的状态，继续保存在repository和working中；
	3. git rm 工程名 -f ➤ 如果一个工程文件已经被修改或者已经放入暂存区，使用-f强制删除。
	4. git rm --cached README ➤如果想从git仓库中移除，同时也在cache暂存区移除了，而保留在当前的目录中，不被跟踪)(通常很多的.gitignore文件)；
- 重命名 git mv  README.md  README
- 查看历史 git log
	-p (--patch)
	-2显示最近两次的更新
	-stat 查看每次提交的简略信息
	![[Pasted image 20230511161802.png]]
	![[Pasted image 20230511161555.png]]
	![[Pasted image 20230511161724.png]]
	![[Pasted image 20230511162026.png]]
---
- 取消
	- 撤销 🌟撤销不可逆🌟git commit --amend
		🌟修补提交，可以让你最后一次提交取消，记住只是最后一次提交
	- 取消暂存
		🌟如何取消工作目录和暂存区已经修改的的文件;
		🌟git reset HEAD file.txt(取消暂存区的file.txt文件)
	- 取消修改 🌟git checkout --contributing.md # 取消对文件的modified；
		🌟这是一个危险的命令，你对那个文件的任何本地修改都会消失，回到最近一次提交的样子；
- 端-git-repository
	🌟简写=远程库网址很长，给他赋予一个代号，容易识别；
	🌟远程库简写，不是值针对一个库，是可以有多个远程库简写同时存在；
	1. 添加远程库：git remote add pb https：//xxxx
	2. git remote # 列出你指定的每一个远程服务器的简写
	3. git remote -v # 读取所有远程库的简写--URL
	4. 拉取远程库：
		- git fetch  remote # fetch只是将远端库数据下载到你的本地仓库，不会自动合并或修改你的工作
		- git pull remote 拉去并合并
		- git fetch 和git pull 一样的命令
---
- 分支
	1. 如果你clone一个远程库，默认简写为origin
		🌟跟踪远程分支：如果你当前分支设置了自动跟踪远程分支，可以使用git pull命令自动抓取后合并该远程分支到当前分支；
		🌟推送到远程分支：git push origin master # 将master分支，推送到远程服务器
		☠当你推送的时候，如果你clone的远程库有变化，你就不能推送成功，你必须先fetch 远端库的数据到本地，将本地的数据进行合并，然后再次推送；
	2. 查看远端库信息：git remote show origin
	3. 远程库的重命名和移除：git remote rename pd paul ;git remote remove paul
- 打标签(版本号)
	1. 列出标签➤git tag or git tag -l(--list) "v1.8.5*"
	2. 创建标签➤
		- 附注标签➤git tag -a v1.4 "my version 1.4"
			🌟git show 显示标签信息与对应的提交信息
		- 轻量标签➤git tag v1.4-lw
			🌟git show 只会显示提交信息
	 3. 后期打标签➤通过git log --pretty=oneline 查看之前的更新
		- git tag -a v1.2 9fceb2(校验的一部分)
	4. 共享标签➤本地创建标签，不会默认在远端显示，需要推送
		🌟git push origin v1.5 #推送单次标签
		🌟git push origin --tags #推送所有本地标签到远端	
	5. 删除标签➤
		🌟删除本地标签(不会影响云端标签)
			 ☯git tag  -d v1.0 #删除本地标签
		🌟删除云端标签
			☯git push origin :refs/tags/v1.0
			☯git push origin --delete v1.0
		
	▪检出标签：就是查看某一之前的标签所处版本的文件内容
		🌟如果你想修改此时的版本文件，你需要在查看的时候，重新创建一个分支，否则不能提交
		🌟git checkout -b Newbranch v1.0 
		🌟修改内容
		🌟提交内容到这个新的分支
			☯ git add
			☯ git commit -m " xxx"
			☯ git push origin Newbranch
- 别名(简称，不是代码联想功能，只是简单替代而已)
	1. 设置的位置➤git config文件
	2. 格式➤git config --global alias.co checkout #co=checkout
				➤git config --global alias.br branch #br=branch
				➤git config --global alias.unstage 'reset HEAD' #unstage=reset HEAD 这个命令是取消暂存
				➤git config --global alias.last 'log -1 HEAD' # 查看最后一次提交 相当于 git last == git log -1 HEAD
🌟分支
	1. git保存数据的方式(每次提交的数据)
		 ▪ Git 仓库中有五个对象：三个 _blob_ 对象（保存着文件快照）、一个 **树** 对象 （记录着目录结构和 blob 对象索引）以及一个 **提交** 对象（包含着指向前述树对象的指针和所有提交信息）
	2. 创建分支➤git branch new_branch #创建一个分支，并不很直接切换到该分支上，而是依然在就的分支上，需要进一步切换分支
	3. 切换分支
		①创建分支git branch testing #创建一个testing的新分支
		②切换分支git checkout testing #切换分支到testing分支上
		③显示分叉历史git log --oneline --decorate --graph --all
	4. 合并分支
		①➤git checkout master
		②➤ git merge hotfix
			▪ ➤这样hotfix分支就合并到master分支上了
		③hotfix分支就不在需要☯删除hotfix分支➤git branch -d hotfix
		▪ 合并冲突：出现冲突以后可使用git status命令查看冲突的位置，可以选择手动合并冲突；
		④合并merge和变基rebase：后者主要是，消除分支的历史记录，看起来历史更加清晰,但是会抹去他人的提交历史，这是不道德的；
	5. 分支管理
		 ▪ git branch #显示所有分支，*的当前默认分支
		 ▪ git branch -v 查看每个分支的最后提交
		 ▪ git branch --merged 查看已经合并的分支
		 ▪ git branch --no-merged 查看未合并的分支
			▪ 在删除未合并的分支时，会提示你使用-D强制删除分支
	6. 分支流的应用
		▪ 主分支main➤develop开发分支➤topic前沿探索分支
		▪ 主分支：稳定正式版；develop开发版；topic创新版
- 远程分支
	 1. 获取远程分支的信息：git remote show；远程分支一般表示为origin/main 对应的你本地代指main
	2. clone远端库：git clone https://xxxx
	3. 拉取 git fetch 从服务器上抓取本地没有的数据，不会修改本地内容
	4. 拉取 git pull 抓取数据并直接合并到本地库分支pull = fetch + merge
	5. 删除远程分支：如果远程的一个分支工作已经完成，并且已经合并到main分支，那么你可以删除这个远程库的分支了：
		git push origin --delete serverfix
		To https://github.com/schacon/simplegit
	5. 跟踪分支(本地跟踪一个远端库的分支)
		- git checkout -b serverfix origin/serverfix
		- git checkout --track origin/master
		- git checkout -b sf origin/serverfix #这表示本地分支跟踪的远端库分支具有不同的名字，本地分支重新起名为sf
		- git branch -u origin/serverfix #修改正在跟踪的上游分支
		- git branch -vv #查看所有的本地分支跟踪的上游分支
		- git fetch --all; git branch -vv #这个和上一个命令不同在于，这会显示你本地每个分支和远端库最新分支的差距，而上一个显示的是本地分支和你最后一次抓取的数据差异
	6. 推送本地分支到远程库
		- git push orgin serverfix #推送本地库serverfix到远程库的serverfix分支
		- git push orgin serverfix：awesomebranch #推送本地库serverfix到远端库，并将这个分支在远端库命名为awesomebranch
---

- 登录
	1. 推送需要登录用户名和密码➤可以通过git config --global credential.helper cache 来设置，这样就不同每次push都需要输入用户名和密码了；
- 第三方服务器
	1. github工作的流程
		- fork repository 
		- 修改
		- 原仓库主人：将自己的仓库作为本地库，你的仓库作为远端库
		- 