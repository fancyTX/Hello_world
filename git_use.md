

# Git学习与使用

## 1.简介
   ### 1.1学习网站  [Git教程--廖雪峰](https://www.liaoxuefeng.com/wiki/896043488029600)
   ### 1.2基本知识
   + 分布式版本控制系统，Linus用C语言开发的
   + 区别于集中式版本控制系统，CVS与SVN等，不集中存放在中央服务器。不必联网，更安全。
   + 只能跟踪文本文件的改动，不能看到其具体改动内容。
   + 暂存区、工作区、版本库。
      + 隐藏目录```.git```为Git的版本库，不算工作区。
        存放stage（或叫index）的暂存区，自动创建的第一个分支`master`，以及指向`master`的一个指针`HEAD`。
      + 把文件往Git版本库里：
        第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；
        第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。
   + 可使用多种协议，如`http、ssh`等，但`ssh`协议速度最快

### 1.3常用指令

[git常用指令](https://liaoxuefeng.gitee.io/resource.liaoxuefeng.com/git/git-cheat-sheet.pdf)



## 2.安装与远程配置

   ### 2.1下载安装
   地址：[windows环境下git安装包下载](https://git-scm.com/download/win)  

   在官网下载github安装包，默认或根据情况一直点击下一步，安装完成。

   ### 2.2配置本地github登录远程仓库
   打开git bash。
 >1. 设置用户名    ```git config --global user.name "yourname"```   ，```--global ``说明本设备所有仓库都使用此配置。
 >
 >2. 设置github账号 ```git config --global user.email "youremail"```   
 >
 >3. 查看当前配置```git config --list```  

 创建本地ssh并连接至服务器
 >1. 获取ssh密钥  ```ssh-keygen -t rsa -C "youremail```  
 >
 >    此时会提示选择ssh-key生成路径，默认即可。密码确认，不输入即可。  
 >
 >2. 打开ssh-key默认路径```C:\Users\23612\.ssh```，复制```id_rsa.pub```文件中的ssh-key。  
 >
 >3. 打开github网站，点击```Setting --- SSH keys --- Add SSH key``` , 输入名称和ssh-key。   
 >
 >4. 回到bash界面,验证配置是否成功```ssh -T git@github.com```
 >
 >    如果连接成功会提示```You've successfully anthenticated```

```
1  git config --global user.name "yourname"
   git config --global user.email "youremail"
2  git config --list
3  ssh-keygen -t rsa -C "youremail
4  ssh -T git@github.com
```

<div align=left><img src="C:\Users\23612\Pictures\Saved Pictures\研究生录取\git1.PNG" style="zoom:50%;" /></div>

<div align=left><img src="C:\Users\23612\Pictures\Saved Pictures\研究生录取\git2.PNG" style="zoom:50%;" />

<div align=left><img src="C:\Users\23612\Pictures\Saved Pictures\研究生录取\git3.PNG" style="zoom:55%;" />

<div align=left><img src="C:\Users\23612\Pictures\Saved Pictures\研究生录取\git5.PNG" style="zoom:60%;" /></div>


## 3.创建本地版本库

+ 创建文件夹，进入目录；
 + 初始化，之后会在当前文件夹下新建一个名叫.git的文件夹，存放git进行版本控制的文件（隐藏文件夹）。
 + 添加有关版本控制的文件,并提交；（每个文件上传后都要提交）
 + 查看当前文件状态；```git status```告诉你文件有被修改过
 + 查看修改部分,会以绿色字标出。```git diff```
```
mkdir git 
mkdir git_repository
git init
git add XXX
git commit -m "message"
git diff
```
<div align=left><img src="C:\Users\23612\Pictures\Saved Pictures\研究生录取\git4.PNG" style="zoom:60%;" /></div>


## 4.添加、删除文件等操作

### 4.1添加文件到库
> 1. 添加文件到仓库。 ```git add git_install.md```
>
> 2. 提交到仓库,```-m```后跟提交说明。  ```git commit -m "增加git安装与配置内容"```
>
>    执行后会显示```X个文件被改动，什么改动```

```git add git_install.md
git add git_install.md
git commit -m "增加git安装与配置内容"
```

 <div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210312153034130.png" alt="image-20210312153034130" style="zoom:60%;" /></div>

### 4.2回退与还原
+ 回退到上一版本```git reset --hard HEAD^```

    <div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210312154431457.png" alt="image-20210312154431457" style="zoom:80%;" /></div>

+ 命令行界面未切换时还原到新版本，用版本号还原，前几位。借用HEAD指针。

    <div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210312154656406.png" alt="image-20210312154656406" style="zoom:80%;" /></div>    

+ 已切换命令行界面时，要用提交号```commit-id```还原。
  
### 4.3撤销修改回到最近一次`git commit`或`git add`时的状态
  + 情况一：还没有被放到暂存区, 现在，撤销修改就回到和版本库一模一样的状态

    `git checkout -- file`

  + 情况二：已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

    ```
    git reset HEAD file
    git checkout -- file
    ```
### 4.4删除文件
+ 从版本库删除
    ```
    git rm file
    git commit -m "删除 git_repository/git_install.md"
    ```
    <div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210312161221470.png" alt="image-20210312161221470" style="zoom:80%;" />

+ 删错了，版本库里还有，把误删的文件恢复到最新版本
    `git checkout -- file`
### 4.5查看历史文件修改记录
+ --pretty=oneline只显示一行
+ commit 后边跟的是版本号，SHA1计算出的。
+ HEAD表示当前版本，上一版本为HEAD^。
  ```
  git log   
  git log --pretty=oneline
  ```
  <div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210312153808675.png" alt="image-20210312153034130" style="zoom:60%;" /></div>
  
### 4.6查看历史指令
`git reflog`

### 4.7配置别名

每个仓库的Git配置文件都放在`.git/config`文件中

`git config --global alias.st status`

<div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210316141006487.png" alt="image-20210316141006487" style="zoom:100%;" />



## 5.远程仓库

### 5.1关联本地仓库与远程仓库
> 1. 在本地或远程新建同名仓库。
> 2. 添加文件到本地仓库。
> 3. 添加远程仓库 。
> 4. 把本地库的所有内容推送到远程库上,`-u`指第一次推送master分支的所有内容。
> 5. 之后，只在本地提交，push即可,不加`-u`。
```
3   git remote add origin https://github.com/fancyTX/Hello_world.git
4   git push -u origin master
5   git push origin master
```
### 5.2删除远程库
只是解除了本地与远程的绑定关系，远程库本身并没有任何改动。
 > 1. 先查看远程库信息 `git remote -v`
 > 2. 再根据名字删除
 ```
1  git remote -v
2  git remote rm origin
 ```
<div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210312165339524.png" alt="image-20210312165339524" style="zoom:80%;" />   

### 5.3从远程库克隆
> 1. 在网页创建新仓库`gitskills`
> 2. 克隆到本地库
> 3. 查看本地库
```
2  git clone https://github.com/fancyTX/gitskills.git 
3  cd gitskills; ls
```
 <div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210312183704228.png" alt="image-20210312183704228" style="zoom:80%;" />



## 6.分支管理

### 6.1什么是分支

一开始的时候，`master`分支是一条线，Git用`master`指向最新的提交，再用`HEAD`指向`master`，就能确定当前分支，以及当前分支的提交点。

每次提交，`master`分支都会向前移动一步，这样，随着你不断提交，`master`分支的线也越来越长。

当我们创建新的分支，例如`dev`时，Git新建了一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上。

Git创建一个分支很快，因为除了增加一个`dev`指针，改改`HEAD`的指向，工作区的文件都没有任何变化！

不过，从现在开始，对工作区的修改和提交就是针对`dev`分支了，比如新提交一次后，`dev`指针往前移动一步，而`master`指针不变。

在`dev`上的工作完成了，就可把`dev`合并到`master`上，把`master`指向`dev`的当前提交，就完成合并。

合并完分支后，甚至可以删除`dev`分支。删除`dev`分支就是把`dev`指针给删掉，删掉后，我们就剩下了一条`master`分支。

### 6.2创建与合并分支
> 1. 查看分支，当前分支前面会标一个`*`号
> 2. 创建并切换分支`dev`(`checkout` 后跟`-b`表示创建并切换)
> 3. 再次查看
> 4. 在分支`dev`上提交：修改某个文件，add ，commit
> 5. 切换回`master`分支,文件不变，因为`master`分支此刻的提交点并没有变
> 6. 合并，把`dev`分支的工作成果合并到`master`分支上，此时为快速合并
> 7. 删除分支`dev`
> 8. 再次查看
```
1  git branch
2  git branch dev; git checkout dev 或 git checkout -b dev
  # 创建并切换可用 git switch -c dev 或 git checkout -b dev
  # 切换分支可用  git switch/branch dev
3  git branch
4  git add readme.txt;git commit -m "branch test"
5  git checkout master
6  git merge dev
7  git branch -d dev
8  git branch
```
 <div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210312195616494.png" alt="image-20210312195616494" style="zoom:80%;" />


+ 分支管理策略
master分支应该是非常稳定,平时不能在上面干活。干活都在dev分支上，dev分支是不稳定的。
  比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
+ 合并分支时两种模式
+ 默认Fast forward模式，删除分支后，会丢掉分支信息，看不出来曾经做过合并。
  
+ 普通模式，合并后的历史有分支，能看出来曾经做过合并。 加上` --no-ff`参数，表示禁用`Fast forward`
```
git merge  -m "merge with off" dev
git merge --no-ff -m "merge with no-ff" dev
```

### 6.3解决分支合并时的冲突
当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

> 1. 创建并切换分支`feature1`
> 2. 修改文件，在分支`feature1`上提交
> 3. 切换回`master`分支，修改，提交
> 4. 合并，两分支各自有新的提交，合并时产生冲突, 提示信息。
```
1  git switch -c feature1
2  git add readme.txt ;git commit -m "AND simple"
   # readme.txt追加"AND simple”
3  git  switch master
   git add readme.txt ;git commit -m "& simple"
   # readme.txt追加"& simple“
4  git merge feature1
```

<div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210312201343018.png" alt="image-20210312201343018" style="zoom:80%;" />

要手动解决冲突，要先找到冲突文件，查看文本信息发现Git自己用`<<<<<<<，=======，>>>>>>>`标记出不同分支的内容, 进行修改。
> 1. 找出冲突文件
> 2. 修改后提交
> 3. 查看分支合并情况（分支合并图）`git log --graph`
> 4. 删除分支`feature1`
```
1  git status
2  git add readme.txt;git commit -m "conflict fixed"
3  git log --graph --pretty=oneline --abbrev-commit
4  git branch -d feature1
```

<div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210312202413272.png" alt="image-20210312202413272" style="zoom:80%;" />
<div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210312201645609.png" alt="image-20210312201645609" style="zoom:80%;" />
<div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210312202621544.png" alt="image-20210312202621544" style="zoom:80%;" />

### 6.4Bug分支

修复Bug时，创建新的bug分支来修复—合并—删除；

> 1. 查看当前分支；
> 2. 暂存工作现场；
> 3. 确定修改bug的分支，创建并切换临时分支；
> 4. 修复bug后提交；
> 5. 切换回原分支，合并删除临时分支；

```
1  git status
2  git stash
3  git checkout master;git checkout -b issue-101
4  vim readme.txt;git add readme.txt;git commit -m "fix bug 101"
5  git switch master;git merge --no-ff -m "merged bug fix 101" issue-101
6  git branch -d issue-101
```

<div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210316101350824.png" alt="image-20210316101350824" style="zoom:80%;" />

先暂存工作现场，然后修复bug，再回到工作现场；

> 1. 暂存工作现场
> 2. 查看工作现场存放在哪里
> 3. 恢复工作现场,两种方式
>    + 恢复后并不删除stash内容，需要用另外指令删除
>    + 恢复的同时把stash内容也删了
> 4. 查看工作现场
>
> 5. 恢复时可指定stash,先查看再指定。

```
1  git stash
2  git stash --list
3  git stash apply;git stash drop 或 git stash pop
4  git stash
5  git stash;git stash apply stash@{0}
```

<div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210316101809880.png" alt="image-20210316101809880" style="zoom:80%;" />

<div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210316102000431.png" alt="image-20210316102000431" style="zoom:80%;" />

在master分支上修复的bug，想要合并到当前dev分支，可只复制所提交的修改，避免重复劳动。

> 1. 查看分支
> 2. 复制特定提交到当前分支

```
1  git branch
2  git cherry-pick commit-id
```

### 6.5Feature分支

添加功能时使用，不影响主分支。

> 1. 查看分支
> 2. 创建feature分支，并切换。进行操作，添加提交。查看分支。
> 3. 切换回来，合并删除；
> 4. 如果取消新功能，要删除分支，并未合并时会删除失败，此时要强制删除，参数-D。

```
1  git branch
2  git switch -c feature-vulcan 
   vim re.txt; git add re.txt; git commit -m "add feature vulcan"
   git status
3  git switch master; git merge feature-vulcan; git branch -d feature-vulcan 
4  git branch -d feature-vulcan
   git branch -D feature-vulcan 
```

<div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210316104023878.png" alt="image-20210316104023878" style="zoom:80%;" />

<div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210316104133615.png" alt="image-20210316104133615" style="zoom:80%;" />

### 6.6多人协作

+ 当从远程仓库克隆时，Git自动把本地的`master`分支和远程的`master`分支对应起来了，并且，远程仓库的默认名称是`origin`。

+ 推送分支。

  就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上。不一定必须推送分支。

  + `master`分支是主分支，因此要时刻与远程同步；
  + `dev`分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
  + bug分支只用于在本地修复bug，就没必要推到远程了
  + feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

+ 抓取分支。

  多人协作时，大家都会往`master`和`dev`分支上推送各自的修改。推送失败，双方推送的提交有冲突。

  + 先用`git pull`把最新的提交从`origin/dev`抓下来，然后本地合并，解决冲突，再推送。
  + 若失败，则没有指定本地`dev`分支与远程`origin/dev`分支的链接，根据提示，设置`dev`和`origin/dev`的链接，再抓取。
  + `git pull`成功，但是合并有冲突，需要手动解决冲突。

> 1. 查看远程库信息；查看详细信息。
>
> 2. 推送分支
> 3. 抓取分支。

```
1  git remote
   git remote -v
2  git push origin master
3  git pull #不行了用：
   git branch --set-upstream-to=<branch-name> origin/<branch-name>; git pull; 
   git add file; gir commit -m "message";
   git push
```

### 6.7rebase

rebase操作的特点：把分叉的提交历史“整理”成一条直线，看上去更直观。缺点是本地的分叉提交已经被修改过了。目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

```
git log --graph --pretty=oneline --abbrev-commit
git rebase
git log --graph --pretty=oneline --abbrev-commit
```

rebase停止

`git rebase  --quit`

发现删除错误，撤销rebase操作：先查看本地记录找到commit-id，然后恢复

`git reflog; git reset --hard commit-id  `

<div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210316155013221.png" alt="image-20210316155013221" style="zoom:80%;" />

## 7.标签管理

+ 标签就是打标签时的版本，其实是版本库的一个快照。是指向某个commit的指针，跟某个commit绑在一起。

+ 默认标签是打在最新提交的commit上的，如果忘记了，可找到历史提交的commit id，然后打上。`git log --pretty=oneline --abbrev-commit`

+ 标签不是按时间顺序列出，而是按字母排序的
+ 创建的标签都只存储在本地，不会自动推送到远程。打错的标签可以在本地安全删除。已推送的：先在本地删除，然后远程删除。

> 1. 查看并切换分支；
> 2. 打标签；用`-a`指定标签名，`-m`指定说明文字;
> 3. 查看所有标签；
> 4. 查看标签信息；
> 5. 删除标签；
> 6. 推送某个标签或全部未推送的标签到远程。

```
1  git branch;  git checkout master;
2  git tag v1.0
   git tag v1.0 commit-id
   git tag -a v1.0 -m "version 1.0 released" commit-id
3  git tag
4  git show v1.0
5  git tag -d v1.0 #本地
   git tag -d v1.0; git push origin :refs/tags/v1.0	#远程
6  git push origin v1.0 #推送标签V1.0
   git push origin --tags  #推送全部标签
```

<div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210316111743775.png" alt="image-20210316111743775" style="zoom:80%;" />

<div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210316111831289.png" alt="image-20210316111831289" style="zoom:80%;" />

<div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210316134036892.png" alt="image-20210316134036892" style="zoom:80%;" />


## 8.Gitee关联

创建本地ssh并连接至服务器

> 1. Gitee网页创建新项目
> 2. 本地关联;若失败：
> 3. 查看已关联同名Github仓库，则先删除。查看远程库信息。
> 4. 同时关联Github和Gitee，先关联Github，远程库叫github，在关联Gitee远程库Gitee。查看。
> 5. 推送注明github或gitee。

```
2  git remote add origin https://gitee.com/fan_xi/hello_world.git
3  git remote -v; 
   git remote rm origin; git remote -v
4  git remote add github git@github.com:fancyTX/Hello_world.git;
   git remote add gitee git@gitee.com:fan_xi/Hello_world.git
   git remote -v
5  git push github master
   git push gitee master
```

<div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210316140403419.png" alt="image-20210316140403419" style="zoom:80%;" />