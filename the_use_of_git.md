## 基本操作
git init		初始化仓库  
git status		查看仓库的状态  
git add			向暂存区中添加文件  
git commit		保存仓库的历史记录  
git log			查看提交日志  
git log --pretty=short	只显示提交信息的第一行  
git log 目录名/文件名		只显示该目录下/与该文件相关的日志  
git log -p		查看提交所带来的改变  
git diff		查看当前工作树与暂存区的差别，如果暂存区没有内容，则只显示工作树与最新提交状态间的差别  
git diff HEAD	查看工作树与最新提交的差别，**因此可以养成执行git commit命令前先执行git diff HEAD来查看本次提交与上次提交之间的差别，HEAD是指向当前分支最新一次提交的指针**
## 分支操作
git branch		显示分支名列表和当前分支  
git checkout -b	xxx	以当前分支为基础创建、切换到分支xxx  
上面这条命令等同于 git branch xxx和git checkout xxx两条命令,前者是创建分支，后者是切换分支
### 合并分支
想要合并到哪个分支，首先要切换到那个分支即 **git checkout xxx**  
然后合并分支，为了在历史记录中**明确记录下本次分支合并，需要创建合并提交，因此在合并时加上 --no-ff参数**，如下：git merge --no-ff 要合并的分支  
随后录入合并提交的信息  
git log --graph		以图标形式查看分支

## 更改提交操作
git reset			回溯历史版本  
要让仓库的HEAD、暂存区、当前工作树状态回溯到指定状态,需要用到 ***git reset --hard hash值***命令。  
**git log**命令只能查看以当前状态为终点的历史日志。而要查看**当前仓库的操作日志**,要使用***git reflog***命令。然后**切换回master分支后再**通过**git reset --hard hash值**回溯历史。  
### 冲突解决
当进行分支合并时,可能会出现冲突。系统会告诉我们**哪些文件发生了冲突**,假设README.md发生了冲突,我们就要解决冲突,所以我们打开README.md文件。  
打开README.md文件后,可以看到其中有=======的标志,在它上面的部分表示**当前HEAD的内容**,下面的部分是**要合并分支中的内容**。更改完内容后进行保存。  
冲突解决后,执行git add XXX与git commit -m ""命令。  
### 修改提交信息
git commit --amend		修改上一条提交信息  
### 压缩历史
如果发现已提交的内容中存在拼写错误等的情况,可以提交一个修改,然后将其包含到前一个提交中,压缩成为一个历史提交。  
1. 修正前面的错误,重新commit内容。  
2. 使用git rebase -i HEAD~2     可以选定**当前分支**中包含**HEAD(最新提交)在内的2个最新历史记录作为对象,并在编辑器中打开**。根据编辑器的说面修改**对应hash值前面的命令**。  

## 推送至远程仓库
git remote add origin git@github.com:用户名/仓库名.git			添加远程仓库,仓库路径为git@github.com:用户名/仓库名.git  
如果想将**当前分支下本地仓库中的内容**推送给远程仓库,需要使用**git push**命令,假设我们在**master**分支下进行操作。  
>git push -u origin master		执行命令后,**当前分支的内容**就会被推送到**远程仓库origin的master分支**。其中-u参数可以在推送的同时,将**origin**仓库的**master分支**设置为**本地仓库当前分支的upstream(上游)**。添加这个参数后,将来运行**git pull**时,本地仓库的这个分支就可以直接从origin的master分支获取内容,省去另外添加参数的麻烦。

>本地的其它分支推送至master以外的分支:
>git checkout -b otherbranch  
>git push -u origin otherbranch

## 从远程仓库获取
git clone git@github.com:用户名/仓库.git				获取远程仓库

>说明:执行 git clone命令后,默认处于**master分支**下,同时origin会自动设置成该远程仓库,也就是说本地仓库的master与Github远程仓库(origin)端的master分支在内容上完全相同。

git branch -a	查看当前分支的相关信息。添加-a参数可以同时显示本地仓库和远程仓库的分支

### 获取远程的其它分支
git checkout -b otherbranch origin/otherbranch

>说明:-b后的第一个参数表示本地仓库中新建分支名称(这里保持了与远程仓库的其它分支名一致),第二个参数表示的是获取来源的分支名称,这里是将远程仓库origin的同名分支作为了来源。

## 获取最新的远程仓库分支
git pull		获取最新的远程仓库中的当前分支
>说明,如果要获取的是远程仓库的其它最新的分支,使用**git pull origin otherbranch**。  

## git pull和git fetch的区别
[详解git pull和git fetch的区别](https://blog.csdn.net/weixin_41975655/article/details/82887273)
