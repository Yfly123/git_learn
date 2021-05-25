## 1.git配置

a. Git config --global user.name 'yangfei'

b. Git config --global user.email 'yf6738@126.com'

2. 创建版本库 (仓库respository)

   a.  mkdir new_content

   b.  cd new_content进入该目录下

   pwd 用于显示当前目录

   c.  创建git可以管理的仓库,  git init
   
3. 创建一个仓库:

   ```
   1、mkdir temp_respo
   2、进入该目录cd temp_respo
   3、git init 把该目录变成git可以管理的仓库
   ```

   

## 2.提交文件

把文件放到new_content 目录下

a. git add git.mad

b. git commit -m "write the file"(引号内是解释说明)

<<<<<<< HEAD
一次可以提交多个文件

```
git add file1.txt
git add file2.txt file3.txt
git commit -m 'change 3 files'
```



## 3.分支管理
>>>>>>> dev

### 3.1创建与合并分支

1.列出分支

```
git branch

  dev
*master
```

2.切换到另一个分支(dev)

```
git checkout dev
```

3.创建新的分支并进入该分支

```
git checkout -b new_dev
```

4.删除分支

```
git branch -D new_dev
```

5.分支合并(在master分支中)

​	将分支合并到主分支上

```
git merge 分支名
```

6.新版分支切换命令switch

创建并切换到分支

```
git switch -c new_dev
```

切换到已有的分支

```
git switch master
```

### 3.2分支冲突

**6.合并冲突**

问题描述：new_dev分支在test.txt中修改为:shanghai

git switch -c new_dev

```
git add test.txt
git commit -m"add shanghai"
```

​					main 主分支中修改test.txt为：shangshan

```
git add test.txt
git commit -m"modify shangshan"
```

git switch main

main 分支中合并分支

```
git merge new_dev
```

出现以下问题：

```
Auto-merging test.txt
CONFLICT (content): Merge conflict in test.txt
Automatic merge failed; fix conflicts and then commit the result.
```

git status 查看冲突

**解决冲突**

```
git add test.txt
git commit -m"conflict fixed"
```

### 3.3分支管理策略

通常，合并分支时，如果可能，Git会用`Fast forward`模式，但这种模式下，删除分支后，会丢掉分支信息。

合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。

### 3.4Bug分支

当你接到一个修复一个代号101的bug的任务时，很自然地，你想创建一个分支`issue-101`来修复它，但是，当前正在`dev`上进行的工作还没有提交：

```
git stash 
```

把当前工作现场储存起来，等以后恢复现场后继续工作。

修复bug后，在main分支上add   commit 后合并分支并删除修复bug用的分支

返回到之前的工作区

git switch dev

git status 发现工作区是干净的

返回之前的工作现场

```
git stash list
```

恢复工作现场

1、方法一

```
git stash apply   stash 内容并不会被删除
git stash drop    删除stash内容
```

2、方法二

```
git stash pop
```

恢复后git stash list就看不到任何内容

恢复指定的stash

```
git stash apply stash@{0}
```

main分支完成后，需要修复dev分支相同的bug

通过

```
git cherry-pick  commit命令（main 分支修复后的commit码）   
```

复制特定的提交到当前分支，这样就不需要在dev分支上手动再把修bug的过程重复一遍。

### 3.4 feature分支

软件开发中，总有无穷无尽的新的功能要不断添加进来。

添加一个新功能时，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。

在feature分支上完成了开发后

```
git switch main
```

main主分支未和feature分支进行合并，此时不需要该分支开发二功能，想删除feature分支(强行删除)

```
git branch -D feature
```

### 3.5多人协作

推送分支

 把本地库该分支提交到远程库

```
git push origin main
```

如果提交其他分支

```
git push origin dev
```

抓取分支

```
git clone git@github.com:michaelliao/learngit.git
```

- 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
- 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
- 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
- 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。

## 4.git查看提交历史

1、git log 

```
git log --oneline  查看历史纪录的简洁版本
git log --graph   查看历史中什么时候出现了分支、合并
git log --reverse  逆向显示所有的日志
git log --author=yangf --oneline -5   只想查找指定用户的提交日志可以使用命令
git log --graph --pretty=oneline --abbrev-commit 分支形式查看
```

指定日期，可以执行几个选项：--since 和 --before，但是你也可以用 --until 和 --after。 --no-merges 选项以隐藏合并提交

```
git log --oneline --before={3.weeks.ago} --after={2010-04-18} --no-merges
```

2、查看指定文件的修改记录

```
git blame file_name
```

以列表形式显示修改记录

## 5.时光机穿梭(修改文件)

### 5.1版本回退

1. 查询状态

```
git status 
```

  2.查询文件被修改的内容

```
git diff git_learn.md 
```

提交修改和提交新文件是一样的步骤：

```
a. git add git_learn.md
b. git commit -m “modify content”
```

  3.查看修改的历史记录

```
git log
```

   4.查看历史命令

```
git reflog
```

   5.版本回退

head 表示当前版本

```
git reset --hard head^(加上^表示上一个版本)
```

^^上上一个版本，^^^上上上一个版本，上100个版本head~100

   **6.暂存区的内容被commit到了仓库，怎么回退**

```
回退到上一次版本：
git reset --hard HEAD^
回退到某一个commit id 时
git reset --hard commit_id
```

   **7.修改的内容在工作区未add到暂存区，怎么删除工作区内容**

```
git checkout -- filename
例如:git chekout -- test.txt
```

   **8.修改的内容被add到了暂存区还未被commit**

```
首先:git reset HEAD test.txt   将暂存区的内容退回到工作区
接着:git checkout -- test.txt  将工作区的内容删除
```



### 5.2工作区和暂存区

**撤销修改**

git checkout --git_learn.md

​	1.一种是修改后还没有被放到暂存区，撤销到与版本库一摸一样的状态

	2. 已经添加到暂存区，又做了修改，撤销修改就回到添加到暂存区后的状态。

**删除文件**

```
rm test.txt
```

1、删除工作区文件后，同时删除版本库中的文件，不恢复

```
git rm test.txt
```

2、删除工作区文件后，想恢复，即将版本库中的文件恢复到工作区

```
git checkout test.txt
```



## 6.远程仓库

1. #### 配置

   git-bash中输入：ssh-keygen -t rsa -C '邮箱'

   ​		id_rsa是私钥;  id_rsa.pub是公钥

   把公钥添加到Github中

   #### 2.把本地仓库与Github库连接并推送

   ​	1.按照github提示，在本地的仓库下运行:git remote add 远程仓库名 git@.....

   ```
git remote add 远程库名 git@github.com:Yfly123/git_learn.git
   git branch -M main
git push -u 远程库名 main
   ```

   ​	2.首次关联远程库:

   ```
git push -u origin main
   ```

   ​     **3.每次修改后可推送到远程仓库**

   ```
git push origin main
   ```

   ​	4.删除远程库与本地库的绑定,远程库本身没有改动

   ```
git remote rm 远程库名字
   ```

    5. 查看远程库信息

       ```
    git remote -v
       ```

   	6. 查看远程库

   ```
git remote
   ```

   #### 3.从远程库克隆

   git clone git@github.com:name/库名.git

   1、从远程库下载新分支和数据

   ```
   git fetch origin
   ```
   
   该命令执行后需要执行git merge 远程分支到本地分支
   
   ```
   git merge origin/master
   ```
   
   
   
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
   
      ```
      git merge --no-ff -m'merge with no ff' dev
      ```
   
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





## 7.标签管理

### 7.1 创建标签

切换到需要打标签的分支上 git switch master

git tag  v1.0  给最新commit提交的版本打印标签

git tag   查看所有标签

git show v1.0  查看标签以及说明文字

找到历史提交的commit id，然后打上标签

```
git log --pretty=oneline --abbrev-commit
```

然后   

```
git tag v1.0 f52c633(commit id)
```

还可以创建带有说明的标签，用`-a`指定标签名，`-m`指定说明文字：

```
git tag -a v1.0 -m 'add tag' 10094db(commit id)
```

### 7.2 操作标签

如果标签错了，可以删除

```
git tag -d v1.0q
```

推送标签到远程

```
git push origin <tag name>
```

一次性推送全部尚未推送到远程的本地标签

```
git push origin --tags
```

如果标签已经推送到远程了，要删除远程标签先从本地删除

```
git tag -d v1.0,
```

然后从远程删除，

```
git push origin :refs/tags/v1.0
```