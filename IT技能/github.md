怎么用github搭建博客 

1. 下载git（我的电脑是windows版本，所以以64位的windows为例）

   地址：  https://git-scm.com/download/win

2. 安装git

    1. 点击exe文件

    2. 点击next

       ![](https://i.loli.net/2020/09/14/ZbRdB5PIYylnFf6.png)

       ![](https://i.loli.net/2020/09/14/tBIsNoAGlMKVgmY.png)

       安装目录可以自己选择

       ![](https://i.loli.net/2020/09/14/ExRmQ5ODh2I7J1M.png)

       安装自己所需要的模块

       ![](https://i.loli.net/2020/09/14/1aD2MQnKSVqYwAW.png)

       选择编辑器

       ![](https://i.loli.net/2020/09/14/ChTrdvUWnYZR5Gs.png)

       使用命令行环境

       然后就是一直next，直至安装完成

   

3. 连接git和github

   右键单击桌面

   ![](https://i.loli.net/2020/09/14/jnGitqwrSzBZYOy.png)
输入命令：
   
   ```
   ssh-keygen
   ```
   
   ![](https://i.loli.net/2020/09/15/78dRUZ6z4YbKMQj.png)
   
   就给出了密钥的地址：
   
   跟着地址找到指定文件夹：

![](https://i.loli.net/2020/09/15/YrGb7f6lPKdgXMU.png)

打开普遍文件，里面有一整串密码，复制粘贴

打开自己的github账号

![](https://i.loli.net/2020/09/15/lpduBr32QgiMvYD.png)

![](https://i.loli.net/2020/09/15/2nNtDaEKZALkjJ8.png)

![](https://i.loli.net/2020/09/15/GMp3CPJS5xfIkRi.png)

将复制的那一串密码粘贴就行了



然后 ：

1. 在电脑上新建文件夹

2. 在文件夹内，右键单击----》git bash here
3. 输入命令：git init

![](https://i.loli.net/2020/09/15/UmGaPcq9oW7y1ZM.png)

4. 连接文件夹和github

   

![](https://i.loli.net/2020/09/15/8c9wH5NsFymJxSW.png)

输入命令：

git pull origin master

![](https://i.loli.net/2020/09/15/SBG1LIFOQg48zD5.png)

此时和文件夹对应的github的仓库的文件已经被下载到电脑上的而文件夹里

![](https://i.loli.net/2020/09/15/hEMOxYe65SpTbJN.png)

简单介绍一下：

![](https://i.loli.net/2020/09/15/hOxm9KRzAvPIUiY.png)

在电脑上的文件夹是我们的工作区

当我们在工作区新增加一个文件的时候，add到暂存区

```
1. git add 文件名
2. git add .//把文件夹下的所有文件
```

```
git commit -m "文件的描述，可以不加"
```

推到远程仓库：

```
git push origin master
```

