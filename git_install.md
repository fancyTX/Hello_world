# Github本地安装、连接服务器、基本操作

## 1、本地安装配置、连接服务器
### 学习网站

[Git教程--廖雪峰](https://www.liaoxuefeng.com/wiki/896043488029600)

### 基本知识

+ 分布式版本控制系统，Linus用C语言开发的

+ 区别于集中式版本控制系统，CVS与SVN等，不集中存放在中央服务器。不必联网，更安全。

+ 只能跟踪文本文件的改动，不能看到其具体改动内容。

+ 暂存区、工作区、版本库。

  + 隐藏目录```.git```为Git的版本库，不算工作区。

    存放stage（或叫index）的暂存区，自动创建的第一个分支`master`，以及指向`master`的一个指针`HEAD`。

  + 把文件往Git版本库里：

    第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；

    第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。

### 下载安装

地址：[windows环境下git安装包下载](https://git-scm.com/download/win)  

在官网下载github安装包，默认或根据情况一直点击下一步，安装完成。

 ### 配置本地github登录远程仓库
 打开git bash。
 >+ 设置用户名    ```git config --global user.name "yourname"```   ，```--global ``说明本设备所有仓库都使用此配置。
 >+ 设置github账号 ```git config --global user.email "youremail"```   
 >+ 查看当前配置```git config --list```  

 创建本地ssh并连接至服务器
 >+ 获取ssh密钥  ```ssh-keygen -t rsa -C "youremail```  
 > 
 > 此时会提示选择ssh-key生成路径，默认即可。密码确认，不输入即可。  
 > 
 >+ 打开ssh-key默认路径```C:\Users\23612\.ssh```，复制```id_rsa.pub```文件中的ssh-key。  
 >
 >+ 打开github网站，点击```Setting --- SSH keys --- Add SSH key``` , 输入名称和ssh-key。   
 >
 >+ 回到bash界面,验证配置是否成功```ssh -T git@github.com```
 >
 >   如果连接成功会提示```You've successfully anthenticated```

<div align=left><img src="C:\Users\23612\Pictures\Saved Pictures\研究生录取\git1.PNG" style="zoom:50%;" /></div>

<div align=left><img src="C:\Users\23612\Pictures\Saved Pictures\研究生录取\git2.PNG" style="zoom:50%;" />

<div align=left><img src="C:\Users\23612\Pictures\Saved Pictures\研究生录取\git3.PNG" style="zoom:55%;" />

<div align=left><img src="C:\Users\23612\Pictures\Saved Pictures\研究生录取\git5.PNG" style="zoom:60%;" /></div>

 ## 2、git基本操作
 ### 创建本地版本库

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

### 关联本地仓库与远程仓库

1. 在本地或远程新建同名仓库。

   <div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210312162335419.png" alt="image-20210312162335419" style="zoom:80%;" />

2. 添加文件到本地仓库

   

### 添加文件到仓库

1. 添加文件到仓库。 ```git add git_install.md```

2. 提交到仓库,```-m```后跟提交说明。  ```git commit -m "增加git安装与配置内容"```

   执行后会显示```X个文件被改动，什么改动```

    <div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210312153034130.png" alt="image-20210312153034130" style="zoom:60%;" /></div>

 

### 基本操作

+ 查看历史修改操作 

  + --pretty=oneline只显示一行
  + commit 后边跟的是版本号，SHA1计算出的。
  + HEAD表示当前版本，上一版本为HEAD^。

  ```
  git log   
  git log --pretty=oneline
  ```

  <div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210312153808675.png" alt="image-20210312153034130" style="zoom:60%;" /></div>

+ 查看历史命令```git reflog``

  

+ 回退与还原

  + 回退到上一版本```git reset --hard HEAD^```

    <div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210312154431457.png" alt="image-20210312154431457" style="zoom:80%;" /></div>

  + 命令行界面未切换时还原到新版本，用版本号还原，前几位。借用HEAD指针。

    <div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210312154656406.png" alt="image-20210312154656406" style="zoom:80%;" /></div>    

  + 已切换命令行界面时，要用提交号```commit-id```还原。

    ```
    git reflog   #先查看commit-id
    git reset --hard commit-id
    ```

    <div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210312155401238.png" alt="image-20210312155401238" style="zoom:80%;" /></div>

+ 撤销修改回到，最近一次`git commit`或`git add`时的状态。 

  + 情况一：还没有被放到暂存区, 现在，撤销修改就回到和版本库一模一样的状态

    `git checkout -- file`

  + 情况二：已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

    ```
    git reset HEAD file
    git checkout -- file
    ```

+ 删除文件

  + 从版本库删除

    ```
    git rm file
    git commit -m "删除 git_repository/git_install.md"
    ```

    <div align=left><img src="C:\Users\23612\AppData\Roaming\Typora\typora-user-images\image-20210312161221470.png" alt="image-20210312161221470" style="zoom:80%;" />

  + 删错了，版本库里还有，把误删的文件恢复到最新版本

    `git checkout -- file`

    

