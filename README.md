# learninggit
just test
---------------------
1.生产密钥
$ ssh-keygen -t rsa -C "ali-yqf@null.com"

2.添加远程仓库
$ git remote add origin git@github.com:RookieFa/learninggit.git

3.把本地资源推到远程仓库
$ git push -u origin master
由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令


# About Branch
. 查看分支：git branch
. 创建分支：git branch <name>
. 切换分支：git checkout <name>
. 创建+切换分支：git checkout -b <name>
. 合并某分支到当前分支：git merge <name>
. 删除分支：git branch -d <name>
