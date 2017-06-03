## First commit

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
	$ git status	# On branch master #
	# Initial commit
	#	nothing to commit (create/copy files and use "git add" to track)
	```
	
* git add——向暂存区中添加文件

	> git add命令将其 加入暂存区(Stage 或者 Index)中。暂存区是提交之前的一个临时区域。

	```
	$ git add README.md 
	$ git status	# On branch master
	```
	
* git commit——保存仓库的历史记录
	
	> git commit命令可以将当前暂存区中的文件实际保存到仓库的历史记录中。通过这些记录，我们就可以在工作树中复原文件。

	* 记述一行提交信息
		
		```
		$ git commit -m "First commit"		[master (root-commit) 9f129ba] First commit			1 file changed, 0 insertions(+), 0 deletions(-) 
			create mode 100644 README.md
		```
		
		 -m 参数后的 "First commit"称作提交信息，是对这个提交的 概述。
		
	* 记述详细提交信息
		
		```
		# Please enter the commit message for your changes. Lines starting		# with '#' will be ignored, and an empty message aborts the commit.		# On branch master #		# Initial commit
	```
	
		请不加 - m，直接执行 g i t c o m m i t命令。执行后编辑器就会启 动，并显示如下结果。
		
	*  中止提交
	
		如果在编辑器启动后想中止提交，请将提交信息留空并直接关闭编 辑器，随后提交就会被中止。
		
	* 查看提交后的状态

		执行完git commit命令后再来查看当前状态。
		
		`$ git status`