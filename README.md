# git_study
练习git 如果创建远程仓库？如何删除仓库？如何建立本地仓库与远程仓库的连接
## 配置本地仓库
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"

## 本地仓库基本操作

第一步 : 在需要git 管理的文件夹下打开git base here 
第二步：在git中进行项目管理的初始化 git init
第三步：在git中创建自己的项目文件
第四步：通过git add * 将所有的项目文件添加进去临时区域内
第五步：通过git commit -m 操作说明  将临时区域内的项目推送到本地的仓库上去
第六步：对项目进行修改之后,可以先看看修改了哪些东西，git diff 
第七步：确认完修改之后，可以通过git commit -a -m 操作说明 来进行上传了.
第八步：如果需要切换版本，只需要通过git reflog 查看下自己的操作历史，然后通过git reset 
--hard 版本号 就可以自由的切换不同的状态了。
第九步: 如需删除文件，使用git rm 文件名 来进行删除,然后通过git commit -a -m 提交
第十步:如果发生在本地误删的情况，可以直接使用git checkout 把临时区域的内容拉到本地





总结：以上的知识只是个人在用的时候本地代码的一个管理而已，并不涉及远程多人共同协作，如果你只是在本地管理代码的话，上面的命令足够你使用了，因为毕竟你知道了如何让自己的代码库添加、删除、和回溯。代码的每一次修改也都会做记录，你可以随时恢复最新的版本和退回老的版本，并且比较每次代码的不同之处，找到原因。

## 本地与远程连接

>简单的说：需要让远程的github 可以连接到你的电脑，是通过电脑的ssh_密钥 知道的。然后就可以建立本地与远程仓库的连接
>第一次推送按照以下步骤执行
**1：创建自己的SSH**
`ssh-keygen -t rsa -C "youremail@example.com"` 你的邮箱是github注册邮箱
>创建自己的ssh密钥，用于跟远程的服务器进行通信，它毕竟得知道这个是你亲自推送的代码才行。
>


**2:在github上找到配置ssh密钥的地方，然后进行新建 并添加电脑上的密钥**
> 在settin/ssh...

**3：创建远程仓库(design_pattern_demo)，或者本地仓库使用命令推送文件**
创建本地仓库 git init 
创建远程创库 design_pattern_demo
将本地与远程创库进行连接

`git remote add origin git@github.com:lian08/design_pattern_demo.git` 将本地与远程创库进行连接
**4:查看是否添加远程仓库成功。**
`git remote -v`
>返回信息如下则是成功
>origin 'git@github.com....xx'

**推送项目**
`git pull origin master`


或者本地仓库代码提交到git@github.com:lian08/design_pattern_demo.git远程仓库中

~~~
git add .
git commit -m '提交'
git push origin master
~~~


## 分支管理
然，你一个人管理代码的情况下，分支是没必要的，它主要体现在多人协同的情况下

Git鼓励大量使用分支：
查看分支：git branch
创建分支：git branch <name>
切换分支：git checkout <name>
创建+切换分支：git checkout -b <name>
合并某分支到当前分支：git merge <name>
删除分支：git branch -d <name>

### 比如
创建一个新的分支，叫做dev
目前我们的操作是在dev 分支上的，自然，我们现在就指向了dev，它跟master没什么关系了。

将DEV分支合并到主分支上去，分支其实就是为了在不影响主代码的情况下进行代码修改，根据实际情况跟最后的版本进行合并。
**这里，我们要考虑一种情况，就是如果我在分支DEV中修改了内容，同时，我又在主分支MASTER中修改了内容，那么它们合并的时候一定会出现问题！！**

这里，不去考虑复杂的合并分支情况，一般我们开发的话，都会在分支上进行开发，确定没问题之后，合并到主分支中去。



### 实际情况的考虑：

远程分支和本地分支

两条分支最好是一一对应的，master分支和dev分支在本地和远程都有两条

创建分支确实挺容易的，也不复杂，这里就不考虑创建分支的成本性了。你可以理解为创建分支就是又创建一个工作区-暂存区-仓库这样的仓库2，现在你就拥有了仓库1，仓库2 了


目前感觉分支的操作都是在本地操作的，也就是针对本地分支的合并啊，在本地合并之后，再往同名的远程分支中push,那远程分支怎么完成合并呢？




>一般我们git clone下网站源码的时候，默认情况下是主分支是有的，但其余的分支是没有的，这时候我们就需要在本地创建新的分支，这些分支对应着远程中的分支，然后将分支中的代码pull到本地去，比如远程的dev 分支要这么操作

git clone SSH地址 克隆整个项目（默认得到的就是主分支，其他分支并没有）
git checkout -b dev  在本地创建分支
git pull origin dev 从远程的DEV分支拉到本地的dev分支
git add ...
Git commit ...
Git push origin dev 修改完毕后传递到远程的dev分支上去

假设远程公共仓库，有一个master和一个dev分支，进行多人协作开发时候（每个人的公钥必须加入到远程账号下，否则无法push）， 每个人都应该clone一份到本地。 但是clone的只是master，如果远程的master和dev一样，没关系；如果不一致，则需要clone出dev分支 git checkout -b dev origin/dev 之后每个人在本地的dev分支上独自开发（最好不要在master上开发）， 开发完成之后push到远程dev git push origin dev。 之后审核人再确定是否合并dev到master。
在进行任何的push 操作之前，一定要先 pull 一下远程的分支代码，毕竟这个分支代码是被很多人修改的，你只有最新的版本才能和自己的修改合并才行。
