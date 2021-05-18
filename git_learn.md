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

## 3.分支管理

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
git branch -d new_dev
```





## 4.时光机穿梭(修改文件)

### 4.1版本回退

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

### 4.2工作区和暂存区

**撤销修改**

git checkout --git_learn.md

​	1.一种是修改后还没有被放到暂存区，撤销到与版本库一摸一样的状态

	2. 已经添加到暂存区，又做了修改，撤销修改就回到添加到暂存区后的状态。

**删除文件**

rm test.txt

git restore test.txt恢复删除的文件

git rm test.txt彻底删除文件

## 5.远程仓库

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
   
   
   
   
   
   
   
   