## 1.git配置

a. Git config --global user.name 'yangfei'

b. Git config --global user.email 'yf6738@126.com'

2. 创建版本库 (仓库respository)

   a.  mkdir new_content

   b.  cd new_content进入该目录下

   pwd 用于显示当前目录

   c.  创建git可以管理的仓库,  git init

## 2.提交文件

把文件放到new_content 目录下

a. git add Git.mad

b. git commit -m "write the file"(引号内是解释说明)

## 3.时光机穿梭(修改文件)

### 3.1版本回退

git status 查询状态

git diff git_learn.md 查询文件被修改的内容

提交修改和提交新文件是一样的步骤：

​	a. git add git_learn.md

​	b. git commit -m'modify content'

git log 查看修改的历史记录

head 表示当前版本，

git reset --hard head^(加上^表示上一个版本)

^^上上一个版本，^^^上上上一个版本，上100个版本head~100

还原原来的某个版本:

​		git reset --hard (commit id)

git reflog 用来记录每一次命令(每次修改的id ,内容)

### 3.2工作区和暂存区

**撤销修改**

git checkout --git_learn.md

​	1.一种是修改后还没有被放到暂存区，撤销到与版本库一摸一样的状态

	2. 已经添加到暂存区，又做了修改，撤销修改就回到添加到暂存区后的状态。

**删除文件**

rm test.txt

git restore test.txt恢复删除的文件

git rm test.txt彻底删除文件

## 4.远程仓库

1. ### 配置

   git-bash中输入：ssh-keygen -t rsa -C '邮箱'

   id_rsa是私钥;  id_rsa.pub是公钥

   把公钥添加到Github中

   2.把本地仓库与Github库连接

   按照github提示，在本地的仓库下运行:git remote add 远程仓库名 git@.....

   首次关联远程库:git push -u origin(远程库名字)  master

   git push origin(远程库名字)  master每次修改后可推送到远程仓库

   git remote rm 远程库名字     删除远程库与本地库的绑定,远程库本身没有改动

   git remote -v 查看远程库信息

   ### 2.从远程库克隆

   git clone git@github.com:name/库名.git

   

   ## 5.分支管理

   1. ### 创建与合并分支

      1. ​	git checkout -b dev（创建dev分支）或者:git switch -c dev；-b表示创建并切换

         ​	上面一句相当于:git branch dev 

         ​								git checkout dev

      2. git branch 查看当前分支，git add.... ;  git commit -m' '...操作后

      3. dev完成了就切换至master 分支git checkout master

      4. 将dev分支的工作合并到master分支 git merge dev

      5. 合并完成后，删除dev分支   git branch -d dev

   切换到已有的分支可以用git switch master

   2. ### 解决冲突

   当别的分支和主分支都对同一行文字或者代码进行修改时，保存后会产生争执，好比作文，大家都改结尾或者开头，就叫冲突。

   出现冲突后执行以下两句：

   ​		git add test.txt

   ​		git commit -m 'modify conflict'
   
   3. ### 分支管理策略
   
      合并的时候采用
   
      git merge --no-ff -m'merge with no ff' dev
   
      禁用fast forward  
   
      master分支十分稳定，用来发布新版本，平时不在上面操作；
   
      dev分支不稳定，比如当1.0版本发布时再和master合并，在master上发布
   
      不同分分支干活，都有自己的分支，时不时往dev分支上合并就可以了
   
   4. ### Bug分支
   
   当前工作过程中，突然遇到另一个BUG需要解决，但是工作没完成，需要保存当前进度，次啊用stash
   
   git stash  把当前工作现场‘储藏起来’，等以后恢复现场继续工作。
   
   具体过程:
   
   1. 当前在dev分支工作，git stash保存现场
   
   2. 回到master分支，git switch master
   
   3. 假如在master分支上修复，那么在master创建临时分支，git checkout -b issue-01
   
   4. 在issue-01分支上修复BUG，然后提交git add test.txt;git commit -m'fixed issue'
   
   5. 修复完成后，切换到master分支，并完成合并，删除issue-01分支
   
      git switch master   ;  git merge --no -ff -m'merge issue-01 bug' issue-01
   
   6. 回到原来工作的分支dev;   git switch dev

工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：

一是用`git stash apply`恢复，但是恢复后，stash内容并不删除，你需要用`git stash drop`来删除；

另一种方式是用`git stash pop`，恢复的同时把stash内容也删了：

5 多人协作

git remote 查看远程库的信息   git remote -v显示更详细的信息

1.  推送分支

把该分支上所有本地推动到远程库git push origin master origin为远程库

如果要推送其他分支,比如dev ，那就git push origin dev 

- `master`分支是主分支，因此要时刻与远程同步；
- `dev`分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
- bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
- feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

2. 抓取分支

   多人协作的工作模式通常是这样：

   1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；
   2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
   3. 如果合并有冲突，则解决冲突，并在本地提交；
   4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！

   如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。

   这就是多人协作的工作模式，一旦熟悉了，就非常简单。





## 6.标签管理

### 6.1 创建标签

切换到需要打标签的分支上 git switch master

git tag  v1.0  给最新commit提交的版本打印标签

git tag   查看所有标签

git show v1.0  查看标签以及说明文字

找到历史提交的commit id，然后打上标签

```
git log --pretty=oneline --abbrev-commit
```

然后   git tag v1.0 f52c633(commit id)

还可以创建带有说明的标签，用`-a`指定标签名，`-m`指定说明文字：

git tag -a v1.0 -m 'add tag' 10094db(commit id)

### 6.2 操作标签

如果标签错了，可以删除

git tag -d v1.0

推送标签到远程git push origin <tag name>

一次性推送全部尚未推送到远程的本地标签

git push origin --tags

如果标签已经推送到远程了，要删除远程标签先从本地删除

git tag -d v1.0,

然后从远程删除，

```
git push origin :refs/tags/v1.0
To github.com:Yfly123/git_test.git
```