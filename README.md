
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
	
		请不加 - m，直接执行 g i t c o m m i t命令。执行后编辑器就会启 动，并显示如下结果。
		
	*  中止提交
	
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