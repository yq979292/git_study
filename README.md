# git工具

## 课程大纲





### 简介

>git 是分布式的代码管理工具

## 本地管理

### 下载安装

[下载地址](http://msysgit.github.io/)



### 全局配置

作用：告诉git是哪一个用户在使用git



~~~
告诉git当前使用的用户是谁

git config --global user.name 'github用户名，也可以是其他名称'

告诉git 绑定的邮箱是什么。

git config --global user.email 'github绑定邮箱'

----------开始使用git-----------
~~~

查看配置

~~~
git config --global user.name 
--->yq979292
git config --global user.email
---->'319281998@qq.com'
~~~



### 初始化仓库

- 1 使用`git bash here `打开`项目工程`
- 2：`git init` 初始化`.git`仓库

~~~~
Initialized empty Git repository in /Users/carreryyan/Desktop/git_init/.git/
---->初始化成功
~~~~

- 3:`git add *`将当前目录下所有文件，全部提交到`暂存区`.也可以使用 `git add 文件路径` 提交某个文件
  - 暂存区是临时存储代码的位置。
  - 可以被追踪到  `git status`
- 4：`git commit -m ”本次提交备注信息“`  将暂存区的内容提交到仓库

~~~
-----------------完成将本地文件提交到仓库---------------------

总结：
第一步：git add 文件路径 或者 git add * 
第二步：git commit -m '提交备注信息'
~~~



**注意：**

- 仓库只能管理当前工程中的的文件。不会管理外部文件
- 与`git_init/.git` ,  `git_init`下所有文件。不管理`git_init`  以外文件
- git add 可以多次添加单个文件，最后在git comit 提交到仓库



>每次修改代码后。某个功能完成结束后，当天下班前，我们需要将代码提交到本地仓库。进行管理和记录。





### 查看文件

#### 查看追踪文件状态

~~~
git status 

查看所有文件状态，新增 删除 更新内容
~~~

**git status 追综的是 修改项目之后，git commit 之前**

#### 查看追踪文件具体修改内容

~~~
git diff <filePaht>

查看具体某个文件。更新哪些内容，新增 或者 删除哪些内容

git diff 
查看所有文件变更记录
~~~

**git diff 追综是，修改了内容之后，git add 之前的状态**



**什么情况是使用：**

- 1：不知道需要 git add 哪些文件
- 2：不知道某个文件更改哪些内容
- 3：不知道当前 新增哪些文件 修改了哪些文件的时候

**git commit 后 没有更新项目，git status  git diff 不会追综到效果的。**



#### 查看提交版本

~~~
git log 查看当前版本提交的记录

git relog  查看历史提交，活跃记录
~~~



### 撤销

### 撤销修改



~~~
`git checkout` 撤销全部的修改文件

git checkout <filePath> 撤销某文件中修改
~~~

**对 git add 之前修改文件，撤销有效**



什么情况下使用：

- 1；修改代码，修改错了。
- 2：合作开发时候，两个人同时修改了一个文件。合并处理时候，检查，查看保留那个人的。不保留可以手动删除可以使用git checkout 撤销

#### 撤销追踪文件（暂存区）修改

**已经git add 如何回退呢**

~~~
get reset head <filePaht>  从暂存区拉回到本地

~~~

练习步骤

- 1修改文件
- 2 git status 
- 3 git add 
- 4:git status
- 5 git reset head  <filepath>
- 6 git status
- 7 git diff
- 8 git checkout  <filePath>



#### 撤销提交仓库的修改

**切换版本实现：**

~~~
git log 查看当前所在版本所有提交激励
git reflog 查看历史记录

git reset --hard '版本id'  切换到任意的版本信息

切换后使用  git reflog 查看历史提交记录
~~~



练习过程

- 1：修改文件；git commit -a  -m '备注'
- 2：get log 查看当前版本所有提交信息 ；获取  版本id
- 3:  找到倒数第二次id  `git reset --hard 'id' 回退到上一个版本`
- 4：git log 查看版本 找到第一次提交的id
- 5:  `git reset --hard 'id'` 回到第一个版本呢
- 6： git reflog 查看历史提交版  找到租后一次提交版本；id 
- 7: `git reset --hard 'id'` 回到最后一次提交版本代码

#### 版本穿梭

~~~
git reset --hard '版本id'
~~~



### 总结

- 1：检查是否配置用户信息

~~~
git config --global user.name
-->xxx
git config --globa user.email
--->xxx@x
~~~

- 2 初始化仓库 ** `git init `**
- 3 将文件添加到暂存区  `git add *  `或者 `git add <filepath>`
- 4 提交到仓库**` git commit -m '备注'`**
- 4:修改内容，**`git status`** 查看文件状态，哪些新增 哪些修改 哪些删除
- 6：查看具体修改不内容 **`git diff <filePath>`**
- 7:  在 add 前撤销修稿 **`git checkout <filePath>`**
- 8:  在add 后撤销  **`git reset head <filePath>`**
- 9:  没问题后  **`git commit -a -m '备注'`** 提交到仓库
- 10: 查看当前版本下的提交记录  **`git log`**
- 11 穿梭版本 **`git reset --hard '版本id'`**
- 12 查看历史记录  **`git reflog`**

### 情景模拟



 初始化项目

~~~
git init 
git add *
git commit -m '注释：什么项目主要是做什么的，开发周期 等一些项目重要信息'
~~~



 某些文件修改时候

**当我在开发时候，更改个别文件；并新建了文件。我有记不住我做过什么？怎么办**？

~~~
1：追踪所有文件的状态。
git status

---> 哪些是新建的文件 哪些文件被修改了


2 如果记不住某个文件修改了哪些内容
git diff 查看所有修改内容
git diff <filePath> 查看某个文件修改了哪些内容

----> 新增哪些代码，删除哪些代码，更新了哪些代码？


3：多次添加修改文件
git add <filePath>

4 完成内容
git commit -m '记录了本次完成内容，问题描述'

~~~



 完成某个功能时候

~~~
git status

对某个修改文件有疑问
git diff <filepath>

有问题撤销

没问题 提交
git commit -a -m '备注'
~~~



 工作一天到点了

 发现添加追综文件出现问题时候

多人合作有人更改你的代码时候



## 分支

### 什么时候用

- 区分运行环境的代码时候使用，master   dev   test
  - Master正式环境下代码。只有领导有去阿奴合并处理
  - test 测试环境下代码
  - dev 开发环境下代码
  - 完成环境区分需要结合远程仓库配体使用。完成git-flow工作流
- 多人合作开发，公共访问一个仓库（远程） 分支表示开发身份



### 分支基本命令

~~~
查看当前仓库有多少分支  

git branch

创建分支
git branch <name>

切换分支
git checkout <name>

创建+切换分支
git checkout -b <name>

合并分支
git merge <name>

删除分支
git branch -d <name>

~~~

#### 模拟多人合作分支使用

- 第一步：将远程仓库拉倒本地  

  ~~~
  git clone '仓库地址'
  ~~~

- 创建分支

- 切换分支

- 开始编写代码

- 提交diamante

- 切换到 master 在合并

- 合并分支

- 删除分支



## 链接远程仓库

#### 如何新建远程仓库





#### 如何建立本地电脑与远程github gitee联系

**通过 `ssh` 建立本地电脑与远程github的联系**

- 1：在本地生成ssh 的秘钥（如果有不需要新建）
- 2：将新建的秘钥，复制到github上，允许我们的github链接我们的电脑

----------------------建立我们的电脑与github通信------------------------

- 3：建立了本地仓库与远程仓库的链接。注意**两个仓库**

~~~~
git remote add orgin git@github.com:yq979292/git_study_delet.git
~~~~

- 4：将本地仓库文件，上传到远程仓库

~~~
实际推送的是master分支上的内容

git push origin master

如果远程分支是 master 可以使用以下命令

git push -u origin master 

将本地提交到远程同时进行分支合并


如果远程不是 master 
git push origin master

刷新远程页面。查案分支 切换分支 查看是否提交成功


能合并分支就合并分支参考文档
https://blog.csdn.net/qq_30607843/article/details/84404000
~~~



## 将远程代码拉到本地



~~~
git pull <远程主机名> <远程分支名>:<本地分支名>

git pull origin master:brantest

~~~

