# Github本地安装、连接服务器、基本操作

## 1、本地安装配置、连接服务器
### 下载安装
地址：[windows环境下git安装包下载](https://git-scm.com/download/win)  
在官网下载github安装包，默认或根据情况一直点击下一步，安装完成。

 ### 配置本地github登录
 打开git bash。
 >+ 设置用户名    ```git config --global user.name "yourname"```   
 >+ 设置github账号 ```git config --global user.email "youremail"```   
 >+ 查看当前配置```git config --list```  
 
 创建本地ssh并连接至服务器
 >+ 获取ssh密钥  ```ssh-keygen -t rsa -C "youremail```  
 此时会提示选择ssh-key生成路径，默认即可。密码确认，不输入即可。  
 >+ 打开ssh-key默认路径```C:\Users\23612\.ssh```，复制```id_rsa.pub```文件中的ssh-key。  
 >+ 打开github网站，点击```Setting --- SSH keys --- Add SSH key``` , 输入名称和ssh-key。   
>+ 回到bash界面,验证配置是否成功```ssh -T git@github.com```,如果连接成功会提示```You've successfully anthenticated```

### 示例
![](https://github.com/fancyTX/Hello_world/blob/main/pictures/git1.PNG)
![](https://github.com/fancyTX/Hello_world/blob/main/pictures/git2.PNG)
![](https://github.com/fancyTX/Hello_world/blob/main/pictures/git3.PNG)
![](https://github.com/fancyTX/Hello_world/blob/main/pictures/git5.PNG)
 ## 2、git基本操作
 ### 创建本地仓库版本库
 + 创建文件夹，进入目录；
 + 初始化，之后会在当前文件夹下新建一个名叫.git的文件夹，存放git进行版本控制的文件（隐藏文件夹）。
 + 添加有关版本控制的文件,并提交；（每个文件上传后都要提交）
 + 查看当前文件状态；
 + 查看修改部分,会以绿色字标出。
```
mkdir git 
mkdir git_repository
git init
git add XXX
git commit -m "备注信息"
git diff
```
### 示例
![](https://github.com/fancyTX/Hello_world/blob/main/pictures/git4.PNG)