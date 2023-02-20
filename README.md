[TOC]

## git 指令

* git init——初始化仓库

	> 执行了 git init命令的目录下就会生成 .git 目 录。这个 .git 目录里存储着管理当前目录内容所需的仓库数据。

	```
	$ mkdir git-tutorial
	$ cd git-tutorial
	$ git init
	 Initialized empty Git repository in /Users/hirocaster/github/github-book /git-tutorial/.git/
	```

* git status——查看仓库的状态

	> git status命令用于显示 Git 仓库的状态
	
	```
	$ git status
	# On branch master #
	# Initial commit
	#
	nothing to commit (create/copy files and use "git add" to track)
	```
	
* git add——向暂存区中添加文件

	> git add命令将其 加入暂存区(Stage 或者 Index)中。暂存区是提交之前的一个临时区域。

	```
	$ git add README.md 
	$ git status
	# On branch master
	```
	
* git commit——保存仓库的历史记录
	
	> git commit命令可以将当前暂存区中的文件实际保存到仓库的历
史记录中。通过这些记录，我们就可以在工作树中复原文件。

	* 记述一行提交信息
		
		```
		$ git commit -m "First commit"
		[master (root-commit) 9f129ba] First commit
			1 file changed, 0 insertions(+), 0 deletions(-) 
			create mode 100644 README.md
		```
		
		 -m 参数后的 "First commit"称作提交信息，是对这个提交的 概述。
		
	* 记述详细提交信息
		
		```
		# Please enter the commit message for your changes. Lines starting
		# with '#' will be ignored, and an empty message aborts the commit.
		# On branch master #
		# Initial commit
	```
	
		请不加 - m，直接执行 git commit命令。执行后编辑器就会启 动，并显示如下结果。
		
	* 一次完成 add 和 commit 两个操作
	
		`git commit -am "评论内容"`
		
	*  终止提交
	
		如果在编辑器启动后想中止提交，请将提交信息留空并直接关闭编 辑器，随后提交就会被中止。
		
	* 查看提交后的状态

		执行完git commit命令后再来查看当前状态。
		
		`$ git status`


---
add 了 testFile 中的修改，没有 add README.md 中的修改，然后直接 commit，用 xcode 打开 readme 直接保存，导致在 MD 中编辑的内容被同步了。T_T
---

* git log——查看提交日志

	git log命令可以查看以往仓库中提交的日志。
	
	* 只显示提交信息的第一行

		`$ git log --pretty=short`
		
	* 显示文件的改动
	
		`$ git log -p`
		
		* 只查看 README.md 文件的提交日 志以及提交前后的差别。

			`$ git log -p README.md`
			
	* git log --graph——以图表形式查看分支

		`$ git log --graph`
		
* git diff——查看更改前后的差别

	> git diff命令可以查看工作树、暂存区、最新提交之间的差别。
	
	* 查看工作树和暂存区的差别

		`$ git diff`
		
	* 查看工作树和最新提交的差别

		`$ git diff HEAD`
		
		**好习惯:在执行git diff HEAD命令，查看本次提交与上次提交之间有什么差别，等 确认完毕后再进行提交。**
		
* git branch——显示分支一览表

	`$ git branch`
	
* git branch -a 查看当前分支的相关信息

	`$ git branch -a`
	
	可以同时显示本地仓库和远程仓库的分支信息
	
*  git checkout -b——创建、切换分支

	`$ git checkout -b feature-A`
		执行下面的命令，创建名为 feature-A 的分支
	
* 切换到 master 分支

	`$ git checkout master`
	
* 切换回上一个分支

	`$ git checkout -`
	
* git merge——合并分支

	* 首先切换到 master 分支
	* 然后合并 feature-A 分支

* git branch -d -- 删除分支
	* $ git branch -d <branchname>

* git reset——回溯历史版本

	`$ git reset --hard 时间节点`
	
* 查看冲突部分并将其解决

	```
	# Git教程	<<<<<<< HEAD - feature-A	=======	- fix-B	>>>>>>> fix-B	```
	
	======= 以上的部分是当前 HEAD 的内容，以下的部分是要合并 的 fix-B 分支中的内容。我们在编辑器中将其改成想要的样子。
	
	```
	# Git教程	- feature-A	- fix-B
	```
	
	冲突解决后，执行git add命令与git commit命令。
	
* git commit --amend——修改提交信息

	`$ git commit --amend`
	
	要修改上一条提交信息
	
	如果保存并退出 vim 编辑界面之后
	提示：
	> error: There was a problem with the editor 'vi'.
Please supply the message using either -m or -F option.

	解决方法：
	> git config --global core.editor /usr/bin/vim
	
	然后再 `$ git commit --amend` 保存并退出就会完成修改
	
* git rebase -i——压缩历史【常用】

	> 在合并特性分支之前，如果发现已提交的内容中有些许拼写错误等， 不妨提交一个修改，然后将这个修改包含到前一个提交之中，压缩成一 个历史记录。
	
	`$ git rebase -i HEAD~2`
	
	> 用上述方式执行 git rebase命令，可以选定当前分支中包含 H E A D(最新提交)在内的两个最新历史记录为对象，并在编辑器中 打开。
	
	```
	pick 7a34294 Add feature-C 
	pick 6fba227 Fix typo
		# Rebase 2e7db6f..6fba227 onto 2e7db6f	# Commands:	# p, pick = use commit	# r, reword = use commit, but edit the commit message	# e, edit = use commit, but stop for amending	# s, squash = use commit, but meld into previous commit	# f, fixup = like "squash", but discard this commit's log message 
	# x, exec = run 	command (the rest of the line) using shell	# These lines can be re-ordered; they are executed from top to bottom. If you 	# remove a line here THAT COMMIT WILL BE LOST.	# However, if you remove everything, the rebase will be aborted.	# Note that empty commits are commented out
	```
	
	将 6fba227 左侧的 pick 部分删除，改写为 fixup。
	
	保存编辑器里的内容，关闭编辑器。
	
* git remote add——添加远程仓库

	* 在 GitHub 上创建的仓库路径为 "git@github.com:wenchao8023/git-tutorial.git"
	* 用 git remote add命令将它设置 成本地仓库的远程仓库 

		`$ git remote add origin git@github.com:github-book/git-tutorial.git`
		
		Git会自动将 git@github.com:github-book/git-tutorial.git远程仓库的 名称设置为 origin(标识符)
		
* git push——推送至远程仓库

	* 推送至 master 分支
		
		> 如果想将当前分支下本地仓库中的内容推送给远程仓库，需要用到 git push命令。现在假定我们在master分支下进行操作
		
		`$ git push -u origin master`
		
		```
		像这样执行git push命令，
		当前分支的内容就会被推送给远程仓库 origin 的 master 分支。
		-u参数可以在推送的同时，将 origin 仓库的 master 分支设置为本地仓库当前分支的 upstream(上游)。
		添加了这个参数，将来 运行 git pull命令从远程仓库获取内容时，
		本地仓库的这个分支就可 以直接从 origin 的 master 分支获取内容，省去了另外添加参数的麻烦
		```
		
	* 推送至 master 以外的分支

		* 除了 master 分支之外，远程仓库也可以创建其他分支。举个例子，我 们在本地仓库中创建 feature-D 分支，并将它以同名形式 push 至远程仓库。			`$ git checkout -b feature-D`
		
		* 我们在本地仓库中创建了 feature-D 分支，现在将它 push 给远程仓 库并保持分支名称不变。	
			`$ git checkout -b feature-D`
			
			```
			it push -u origin feature-D
			Total 0 (delta 0), reused 0 (delta 0)
			To github.com:wenchao8023/git-tutorial.git
			 * [new branch]      feature-D -> feature-D
			Branch feature-D set up to track remote branch feature-D from origin.
			```
			
			现在，在远程仓库的 GitHub 页面就可以查看到 feature-D 分支了。
			
*  git clone——获取远程仓库

	`git clone git@github.com:wenchao8023/git-tutorial.git`
	
	* 查看

		```
		$ git branch -a * master		remotes/origin/HEAD -> origin/master 
		remotes/origin/feature-D
		 remotes/origin/master
		```
		
	* 获取远程的 feature-D 分支

		`git checkout -b feature-D origin/feature-D`
		
		b 参数的后面是本地仓库中新建分支的名称。为了便于理解，我 们仍将其命名为 feature-D，让它与远程仓库的对应分支保持同名。
		
* git pull——获取最新的远程仓库分支
		
	```
	现在我们放下刚刚操作的目录，回到原先的那个目录下。
	这边的本地仓库中只创建了 feature-D 分支，并没有在 feature-D 分支中进行任何提交。
	然而远程仓库的 feature-D 分支中已经有了我们刚刚推送的提交。
	这时我们就可以使用git pull命令，将本地的feature-D分支更新到最新 状态。
	【注意】当前分支为 feature-D 分支。
	```
	
	`git pull origin feature-D`
	
	**多名开发者在同一个分支中进行作业时，为减少冲突情况的发生，建议更频繁地进行 push 和 pull 操作。**
	
	
## 【tips】

1. 解决 UserInterfaceState.xcuserstate 文件带来的影响

	* 退出xcdoe（避免删除该文件之后又产生，造成忽略失败）
	* 打开终端（Terminal），进入到你的项目目录下
	* 使用命令：
		`git rm --cached *.xcuserstate`


