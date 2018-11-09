```
$ mkdir learngit  //创建文件夹
$ cd learngit     //进入
$ pwd             //查看当前目录
$ git init        //把该目录变为git可管理的目录（初始化）
$ vi 文件名        //编辑内容
$ git add 文件名1  //把文件1添加到仓库
$ git add 文件名2  //把文件2添加到仓库
$ git commit -m"提交说明" //把文件提交到仓库
$ git status      //查看仓库当前状态
$ git diff 文件名  //查看不同
$ git log         //从最近到最远的提交日志
$ git log --pretty=oneline  
$ git reset --hard HEAD^ //回退到上一版本
$ cat  文件名      //查看文件内容
$ git reset --hard 1094a  //回退到指定版本
$ git reflog      //记录每一次命令
$ git diff HEAD -- readme.txt //查看工作区和版本库里面最新版本的区别
$ git checkout -- readme.txt //丢弃工作区的修改（恢复工作区）
$ git reset HEAD readme.txt //把暂存区的修改撤销掉（unstage），重新               								 放回工作区
$ rm test.txt     //在文件管理器中把没用的文件删了
$ git rm test.txt //从版本库中删除该文件
/*远程仓库*/
$ ssh-keygen -t rsa -C "youremail@example.com" //创建SSH Key
$ git remote add origin git@github.com:sunjunzhou/learngit.git
                 //本地仓库与远程仓库关联
$ git push -u origin master //第一次把本地库的所有内容推送到远程库上
$ git push origin master  //把本地master分支的最新修改推送至GitHub
$ git clone git@github.com:sunjunzhou/gitskills.git
                 //克隆一个本地库
$ git branch     //查看分支
$ git branch <name> //创建分支
$ git checkout <name>  //切换分支
$ git checkout -b <name> //创建+切换分支
$ git merge <name> //合并某分支到当前分支
$ git branch -d <name> //删除分支
$ git log --graph --pretty=oneline --abbrev-commit 
                       //分支的合并情况
$ git merge --no-ff -m "merge with no-ff" dev  
                 //合并分支禁用Fast forward
$ git stash      //把当前工作现场“储藏”起来
$ git stash list //查看工作现场列表
$ git stash apply//恢复现场
$ git stash drop //删除现场
$ git stash pop  //恢复的同时把stash内容也删了
$ git stash apply stash@{0}  //恢复指定的stash
$ git branch -d feature-vulcan //删除指定分支
$ git branch -D <name>  //丢弃一个没有被合并过的分支，强行删除
$ git remote     //查看远程库的信息
$ git remote -v  //显示更详细的信息
$ git push origin master
//推送分支，就是把该分支上的所有本地提交推送到远程库，推送时要指定本地分支
$ git checkout -b dev origin/dev  //创建远程origin的dev分支到本地
$ git pull      //把最新的提交从origin/dev抓下来
$ git branch --set-upstream-to=origin/dev dev
                //设置dev和origin/dev的链接
$ git rebase    //把分叉的提交历史“整理”成一条直线，看上去更直观。缺点是本地的分叉提交已经被修改过了。
$ git tag v1.0  //当前分支打标签
$ git tag       //查看所有标签
$ git log --pretty=oneline --abbrev-commit
$ git tag v0.9 f52c633  //指定提交打标签
$ git show v0.9   //查看标签信息
$ git tag -a v0.1 -m "version 0.1 released" 1094adb
            //创建带有说明的标签，用-a指定标签名，-m指定说明文字
$ git tag -d v0.1  //删除标签
$ git push origin v1.0  //推送某个标签到远程
$ git push origin --tags  //一次性推送全部尚未推送到远程的本地标签
$ git tag -d v0.9 //如果标签已经推送到远程，要删除远程标签就先从本地删除
$ git push origin :refs/tags/v0.9 //然后，从远程删除。
$ git config --global color.ui true //让Git显示颜色，会让命令输出看     
										起来更醒目
```

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")

$ git add readme.txt

$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    modified:   readme.txt
$ git commit -m "add distributed"

$ git status
On branch master
nothing to commit, working tree clean
```

```
$ git log
commit 1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master)
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:06:15 2018 +0800

    append GPL

commit e475afc93c209a690c39c13a46716e8fa000c366
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:03:36 2018 +0800

    add distributed

commit eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 20:59:18 2018 +0800

    wrote a readme file
    
$ git log --pretty=oneline
1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master) append GPL
e475afc93c209a690c39c13a46716e8fa000c366 add distributed
eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0 wrote a readme file
```

![0](/Users/sunjunzhou/Desktop/0.jpg)

​           第一次修改 -> `git add` -> 第二次修改 -> `git add` -> `git commit`

命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：

一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。



```
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    modified:   readme.txt
    
$ git reset HEAD readme.txt
Unstaged changes after reset:
M    readme.txt

$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   readme.txt
$ git checkout -- readme.txt

$ git status
On branch master
nothing to commit, working tree clean
```

```
$ rm test.txt

$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    deleted:    test.txt

no changes added to commit (use "git add" and/or "git commit -a")

$ git rm test.txt
rm 'test.txt'

$ git commit -m "remove test.txt"
[master d46f35e] remove test.txt
 1 file changed, 1 deletion(-)
 delete mode 100644 test.txt

//误删时
$ git checkout -- test.txt
/*git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。*/
```

远程仓库：

第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

你需要把邮件地址换成你自己的邮件地址，一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。如果一切顺利的话，可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容：![1](/Users/sunjunzhou/Desktop/1.png)

点“Add Key”，你就应该看到已经添加的Key：![3](/Users/sunjunzhou/Desktop/3.png)

为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。





把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。



### SSH警告

当你第一次使用Git的`clone`或者`push`命令连接GitHub时，会得到一个警告：

```
The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?
```

这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入`yes`回车即可。Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：

```
Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
```

这个警告只会出现一次，后面的操作就不会有任何警告了。

如果你实在担心有人冒充GitHub服务器，输入`yes`前可以对照[GitHub的RSA Key的指纹信息](https://help.github.com/articles/what-are-github-s-ssh-key-fingerprints/)是否与SSH连接给出的一致。



git clone

你也许还注意到，GitHub给出的地址不止一个，还可以用`https://github.com/michaelliao/gitskills.git`这样的地址。实际上，Git支持多种协议，默认的`git://`使用ssh，但也可以使用`https`等其他协议。

使用`https`除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用`ssh`协议而只能用`https`。



### 分支策略

在实际开发中，我们应该按照几个基本原则进行分支管理：

首先，`master`分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

那在哪干活呢？干活都在`dev`分支上，也就是说，`dev`分支是不稳定的，到某个时候，比如1.0版本发布时，再把`dev`分支合并到`master`上，在`master`分支发布1.0版本；

你和你的小伙伴们每个人都在`dev`分支上干活，每个人都有自己的分支，时不时地往`dev`分支上合并就可以了。

所以，团队合作的分支看起来就像这样：

![4](/Users/sunjunzhou/Desktop/4.png)





### 推送分支

并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？

- `master`分支是主分支，因此要时刻与远程同步；
- `dev`分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
- bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
- feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

总之，就是在Git中，分支完全可以在本地自己藏着玩，是否推送，视你的心情而定



多人协作的工作模式通常是这样：

1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！

如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。