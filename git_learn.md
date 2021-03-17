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

