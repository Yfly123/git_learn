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

git status 查询状态

git diff git_learn.md 查询文件被修改的内容

提交修改和提交新文件是一样的步骤：

​	a. git add git_learn.md

​	b. git commit -m'modify content'

git log 查看修改的历史记录

head 表示当前版本，