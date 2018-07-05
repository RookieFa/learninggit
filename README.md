# GIT
***

## 初始化

因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。

*注意`git config`命令的`--global`参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。*
``` git
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

## 创建版本库
初始化一个Git仓库，使用`git init`命令。

添加文件到Git仓库，分两步：
* 第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；

使用命令`git add <file>`，注意，可反复多次使用，添加多个文件

* 第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。
* 使用命令`git commit -m <message>`，完成。

## 查看状态

* 要随时掌握工作区的状态，使用`git status`命令
* 如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容

### 版本回退
* `git log`命令显示从最近到最远的提交日志，如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`--pretty=oneline`参数
``` git
$ git log --pretty=oneline
9440fd41ce1934551aea3dc7b4538b795d3853b4 (HEAD -> master, origin/master, origin/HEAD) modified图片
212ffc1dc3e817884fb50a9d80763718c8803a2d learn Markdown
f9c67afc0fe5752daf9485acab2bc711e65c01b6 (origin/develop) edit branch
26b7bd83ad7f36bd3ab5eb3a29b7078c7525f312 branch
cf5b7fa948bb4d2d4cf51704ccd96faf4b371b99 Update README.md
9504c058b9191830985ea178aee35f5818f7e114 生产密钥指令
93d69ac0b516c5bf51b8981d54806998b67503bf Initial commit
```

Git必须知道当前版本是哪个版本，在Git中，用`HEAD`表示当前版本，也就是最新的提交`9440fd4...`，上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个^比较容易数不过来，所以写成`HEAD~100`。

现在，我们要把当前版本`modified图片`回退到上一个版本`learn Markdown`，就可以使用`git reset`命令：
```
$ git reset --hard HEAD^
HEAD is now at 212ffc1 learn Markdown
```
* `HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。
* 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。
* 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本


### 撤销修改
命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：

*(`git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除)*
* 一种是`readme.txt`自修改后还**没有被放到暂存区**，现在，撤销修改就回到和版本库一模一样的状态；
* 一种是`readme.txt` __已经添加到暂存区__ 后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。


用命令`git reset HEAD <file>`可以把暂存区的修改撤销掉（unstage），重新放回工作区

1. 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。
2. 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD <file>`，就回到了场景1，第二步按场景1操作。


### 删除文件
* 命令`git rm`用于删除一个文件

***

## 远程仓库
* 创建SSH Key

`$ ssh-keygen -t rsa -C "ali-yqf@null.com"`

* 添加远程仓库

`$ git remote add origin git@github.com:RookieFa/learninggit.git`

* 推送本地仓库内容到远程仓库
`git push -u origin master` 

**注意:** 由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令`git push origin master`。

***
## 分支管理

* 查看分支：git branch
* 创建分支：git branch <name>
* 切换分支：git checkout <name>
* 创建+切换分支：git checkout -b <name>
* 合并某分支到当前分支：git merge <name>
* 删除分支：git branch -d <name>
