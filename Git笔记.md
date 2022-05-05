## Git

### Git快捷键

1、ctrl+L 清空页面

#### vim常用快捷键

**注意**：使用快捷键需要推出编辑模式

##### 退出

:q 不保存退出

**:q! 不保存强制退出**

**:wq 保存退出，w表示写入，无论是否修改，都会改变时间戳**

:w 保存退出，如果内容未更改，不会更改时间戳

##### 编辑

**2、i  进入编辑模式**

**3、esc 退出编辑模式**

4、

5、**dd: 删除光标所在行**

6、 **yy: 复制光标所在行**

7、 p: 当前光标下粘贴

8、 **u: 编辑后，可以撤回操作**

9、gg: 将光标定位到文件头

10、shift+g: 将光标定位到文件尾 

12、 $: 将光标定位到行尾

13、^:将光标定位到行首

14、 /: 斜杠，再输入字符test，可以向下搜索字符test   后按键n  向下重复键字符test 

15、 ？: 问号，再输入字符test2，可以向上搜索字符test2, 后按键n  向下重复键字符test2

16、**o: 新建一行，并进入输入模式**

17、ggVG：全选 

18、gg+YG: 全选并复制

19、＝＝ :格式化当前行

20、gg=G :格式化整个文档

21、#= :格式当前行及接下来的＃行代码，例如“2=” 格式化当前行及接下来的2行

22、   全部删除：按esc键后，先按gg（到达顶部），然后dG

23、全部复制：按esc键后，先按gg，然后ggyG 24、全选高亮显示：按esc键后，先按gg，然后ggvG或者ggVG

25、单行复制：按esc键后, 然后yy

26、单行删除：按esc键后, 然后dd

27、粘贴：按esc键后, 然后p



### Git工作机制

#### 工作区

写代 码的地方，在电脑的文件夹里面，可以删除

#### 暂存区

临时存储文件，可以删除

#### 本地库

存各种历史版本，一旦上传不能删除



### Git常用命令

#### 基本命令

cd 文件夹名

进入指定的目录

1、  git config --global user.name 用户名   

设置用户标签，只需要设置一次

2、  git config --global user.email 邮箱   

设置用户标签，只需要设置一次

3、git init  

初始化本地库

4、git status 

查看本地库状态

#### 暂存区操作

5、git add 文件名

将指定文件名添加到暂存区 

6、git rm --cached 文件名

将指定文件从暂存区删除

#### 本地库操作

7、git commit -m "日志信息" 文件名

将指定的文件上传到本地库

#### 查看历史版本

8、git reflog 

查看版本信息

9、git log

查看版本详细信息

#### 操作文件

10、cat 文件名

查看文件内容

11、vim 文件名

编辑文件内容

#### 版本穿梭

git reset --hard 版本号  



### Git分支操作

#### 创建分支

git branch 分支名

#### 查看分支

git branch -v

#### 切换分支

git checkout 分支名

#### 合并分支

git merge 分支名

##### 产生冲突

当两个分支的文件都进行了修改，合并时不知道该保存谁的版本，就会发生冲突，必须人为解决

修改master分支

```cmd
zsq@zsq MINGW64 /d/git-Space/git-demo (master)
$ vim hello.txt

hello zsq! hello git22222
hello zsq! hello git33333
hello zsq! hello git44444
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git



zsq@zsq MINGW64 /d/git-Space/git-demo (master)
$ git add hello.txt

zsq@zsq MINGW64 /d/git-Space/git-demo (master)
$ git commit -m "Eight" hello.txt
[master 29556fd] Eight
 1 file changed, 1 insertion(+), 1 deletion(-)


```

修改hot-fix分支

```cmd
zsq@zsq MINGW64 /d/git-Space/git-demo (master)
$ git checkout hot-fix
Switched to branch 'hot-fix'

zsq@zsq MINGW64 /d/git-Space/git-demo (hot-fix)
$ vim hello.txt

hello zsq! hello git22222
hello zsq! hello git33333
hello zsq! hello git55555
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git


zsq@zsq MINGW64 /d/git-Space/git-demo (hot-fix)
$ git add hello.txt

zsq@zsq MINGW64 /d/git-Space/git-demo (hot-fix)
$ git commit -m "nie" hello.txt
[hot-fix a87e976] nie
 1 file changed, 1 insertion(+), 1 deletion(-)

zsq@zsq MINGW64 /d/git-Space/git-demo (hot-fix)
$ git checkout master
Switched to branch 'master'

```

合并

冲突产生的表现：后面状态为 MERGING

```cmd
zsq@zsq MINGW64 /d/git-Space/git-demo (master)
$ git merge hot-fix
Auto-merging hello.txt
CONFLICT (content): Merge conflict in hello.txt
Automatic merge failed; fix conflicts and then commit the result.

zsq@zsq MINGW64 /d/git-Space/git-demo (master|MERGING)
$

```



##### 解决冲突

编辑有冲突的文件，删除特殊符号，决定要使用的内容 

特殊符号：<<<<<<< HEAD 当前分支的代码 ======= 

​					 ======= 合并过来的代码 >>>>>>> hot-fix 

```cmd

hello zsq! hello git22222
hello zsq! hello git33333
<<<<<<< HEAD
hello zsq! hello git44444
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
=======
hello zsq! hello git55555
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
>>>>>>> hot-fix
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
```

修改后

```cmd
hello zsq! hello git22222
hello zsq! hello git33333
hello zsq! hello git44444
hello zsq! hello git55555
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
```

保存在本地库

**注意**：执行提交（注意：此时使用 git commit 命令时不能带文件名）

```cmd
zsq@zsq MINGW64 /d/git-Space/git-demo (master|MERGING)
$ git add hello.txt

--执行提交（注意：此时使用 git commit 命令时不能带文件名）--
zsq@zsq MINGW64 /d/git-Space/git-demo (master|MERGING)
$ git commit -m "zsq1" hello.txt
fatal: cannot do a partial commit during a merge.

zsq@zsq MINGW64 /d/git-Space/git-demo (master|MERGING)
$ git commit -m "zsq1"
[master 152facd] zsq1

--解决冲突后恢复正常状态master--
zsq@zsq MINGW64 /d/git-Space/git-demo (master)
$

```



## GitHab操作

### 须知

GitHab网址：https://github.com/[ ](https://github.com/)



### 远程库操作

#### 创建远程库步骤

1、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052009509.png" alt="image-20220415164019479" style="zoom:80%;" />



2、

  <img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052010786.png" alt="image-20220415164657773" style="zoom: 67%;" />

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052010289.png" alt="image-20220415165209696" style="zoom:80%;" />

#### 创建远程库别名

##### 语法

git remote -v

查看当前所有远程库别名



git remote add 别名 远程库地址

创建远程库别名

**注意**：别名之间不能有空格

##### zsq实操

```cmd
zsq@zsq MINGW64 /d/git-Space/git-demo (master)
$ git remote -v

--别名之间不能有空格--
zsq@zsq MINGW64 /d/git-Space/git-demo (master)
$ git remote add git-demo https://github.com/zgkszsqdyy/git-demo1.git

zsq@zsq MINGW64 /d/git-Space/git-demo (master)
$ git remote -v
git-demo        https://github.com/zgkszsqdyy/git-demo1.git (fetch)
git-demo        https://github.com/zgkszsqdyy/git-demo1.git (push)

zsq@zsq MINGW64 /d/git-Space/git-demo (master)
$ 
```

#### 将本地分支推送到远程库

##### 语法

git push 别名 分支



##### zsq实操

```cmd
zsq@zsq MINGW64 /d/git-Space/git-demo (master)
$ git push git_demo1 master
Enumerating objects: 51, done.
Counting objects: 100% (51/51), done.
Delta compression using up to 12 threads
Compressing objects: 100% (34/34), done.
Writing objects: 100% (51/51), 3.76 KiB | 770.00 KiB/s, done.
Total 51 (delta 16), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (16/16), done.
To https://github.com/zgkszsqdyy/git_demo1.git
 * [new branch]      master -> master

```



#### 从远程库拉取到本地库

##### 语法

git pull 别名 分支

##### zsq实操

```cmd
zsq@zsq MINGW64 /d/git-Space/git-demo (master)
$ git pull git_demo1 master
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 644 bytes | 32.00 KiB/s, done.
From https://github.com/zgkszsqdyy/git_demo1
 * branch            master     -> FETCH_HEAD
   152facd..db5a7b3  master     -> git_demo1/master
Updating 152facd..db5a7b3
Fast-forward
 hello.txt | 1 +
 1 file changed, 1 insertion(+)

```



#### 从远程库克隆到本地库

##### 语法

git clone 远程地址

##### 结果

clone 会做如下操作。1、拉取代码。2、初始化本地仓库。3、创建别名

```cmd
zsq@zsq MINGW64 /d/git-zsq/git_demo1 (master)
$ cat hello.txt

hello zsq! hello git22222
hello zsq! hello git33333
hello zsq! hello git44444
hello zsq! hello git55555
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
hello zsq! hello git
11111111111111111111

zsq@zsq MINGW64 /d/git-zsq/git_demo1 (master)
$ git remote -v
origin  https://github.com/zgkszsqdyy/git_demo1.git (fetch)
origin  https://github.com/zgkszsqdyy/git_demo1.git (push)

```



#### 团队协作

##### 拉取成员

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052011712.png" alt="image-20220417103150698" style="zoom: 67%;" />

<img src="C:\Users\zsq\AppData\Roaming\Typora\typora-user-images\image-20220417103222525.png" alt="image-20220417103222525" style="zoom: 67%;" />



<img src="C:\Users\zsq\AppData\Roaming\Typora\typora-user-images\image-20220417103436030.png" alt="image-20220417103436030" style="zoom: 67%;" />

复制地址并通过微信钉钉等方式发送给该用户，复制内容如下：

![image-20220417103623265](https://gitee.com/js199000124/photo/raw/master/%20images/202205052011474.png)

​          

***在 **atguigulinghuchong** 这个账号中的地址栏复制收到邀请的链接，点击接受邀请。                                                                                                                                                                                                                                                                                                               

​                        ![image-20220417103739909](https://gitee.com/js199000124/photo/raw/master/%20images/202205052011618.png)                                                                                                                                                                                                                                                                                              

##### 成员操作文件

**1**、克隆远程库文件到本地

git clone 远程地址



**2**、编辑文件

vim 文件名



**3**、将编辑好的文件上传到本地库并push到远程库

git push 远程地址(别名) 分支



**4**、其他成员将文件pull到本地库保持本地库和远程和库一致

git pull 远程地址(别名) 分支



#### 跨团队协作

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052011647.png" alt="image-20220417111536961" style="zoom:67%;" />

<img src="C:\Users\zsq\AppData\Roaming\Typora\typora-user-images\image-20220417111642798.png" alt="image-20220417111642798" style="zoom:67%;" />



## idea集成Git

### 环境搭建

#### 创建忽略文件规则

##### 1、创建 git.ignore在用户目录下

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052011814.png" alt="image-20220417121437405" style="zoom:67%;" />

git.ignore内容

```toml
# Compiled class file 
*.class 
 
# Log file 
*.log 
 
# BlueJ files 
*.ctxt 
 
# Mobile Tools for Java (J2ME) 
.mtj.tmp/ 
 
# Package Files # 
*.jar 
*.war 
*.nar 
*.ear 
*.zip 
*.tar.gz 
*.rar 
 
# 	virtual 	machine 
http://www.java.com/en/download/help/error_hotspot.xml hs_err_pid* 
 
.classpath 
.project .settings target .idea 
*.iml 	crash 	logs,  	see 

```

##### 2、在.gitconfig 文件中引用忽略配置文件

1、位置

在用户加目录下

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052011260.png" alt="image-20220417121724135" style="zoom:50%;" />

2、内容

配置地址

```toml
[user]
	name = zsq
	email = 2448712607@qq.com

[core]
    excludesfile = C:/Users/zsq/git.ignore 
```



#### idea定位Git

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052012379.png" alt="image-20220417122346120" style="zoom:50%;" />



#### 初始化本地库

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052012686.png" alt="image-20220417141144204" style="zoom:50%;" />



<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052012833.png" alt="image-20220417141225730" style="zoom:50%;" />

### 添加暂存区和本地库

#### 添加到暂存区

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052012809.png" alt="image-20220417141406519" style="zoom:50%;" />

#### 添加到本地库

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052012560.png" alt="image-20220417141455332" style="zoom:50%;" />

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052012829.png" alt="image-20220417141654435" style="zoom:50%;" />



### 切换版本

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052012620.png" alt="image-20220417142838052" style="zoom:67%;" />

### 分支操作

#### 创建分支

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052012847.png" alt="image-20220417143711481" style="zoom: 67%;" />

#### 切换分支

<img src="C:\Users\zsq\AppData\Roaming\Typora\typora-user-images\image-20220417143851960.png" alt="image-20220417143851960" style="zoom:80%;" />

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052013348.png" alt="image-20220417144039656" style="zoom: 67%;" />

### 合并操作

#### 正常合并

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052013665.png" alt="image-20220417145905227" style="zoom:67%;" />

#### 合并冲突

1、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052013820.png" alt="image-20220417154017820" style="zoom:67%;" />

2、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052013109.png" alt="image-20220417154502833" style="zoom:67%;" />

3、<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052013289.png" alt="image-20220417154619832" style="zoom:67%;" />



## idea集成GitHab

### 设置GitHab账号

1、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052013850.png" alt="image-20220417160636294" style="zoom:67%;" />

2、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052013858.png" alt="image-20220417160741413" style="zoom:67%;" />



3、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052013136.png" alt="image-20220417160821900" style="zoom:67%;" />

4、获取个人令牌

4.1、登陆自己的githab账号

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052014189.png" alt="image-20220417160929073" style="zoom:50%;" />

4.2

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052014682.png" alt="image-20220417161126795" style="zoom:50%;" />

4.3

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052014898.png" alt="image-20220417161357569" style="zoom:50%;" />

4.4

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052014940.png" alt="image-20220417161631750" style="zoom:50%;" />



### 将项目分享到GitHab

1、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052014342.png" alt="image-20220417163840174" style="zoom:67%;" />

2、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052014122.png" alt="image-20220417164334596" style="zoom:67%;" />

### push到GitHab

#### 注意

push 是将本地库代码推送到远程库，如果本地库代码跟远程库代码版本不一致， push 的操作是会被拒绝的。也就是说，要想 push 成功，一定要保证本地库的版本要比远程库的版本高！因此一个成熟的程序员在动手改本地代码之前，一定会先检查下远程库跟本地代码的区别！如果本地的代码版本已经落后，切记要先 pull 拉取一下远程库的代码，将本地

代码更新到最新以后，然后再修改，提交，推送！ 

#### 步骤

1、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052014394.png" alt="image-20220417165058888" style="zoom:50%;" />

2、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052014032.png" alt="image-20220417165519701" style="zoom:50%;" />



### pull到本地库

#### 注意

push 是将本地库代码推送到远程库，如果本地库代码跟远程库代码版本不一致， push 的操作是会被拒绝的。也就是说，要想 push 成功，一定要保证本地库的版本要比远程库的版本高！因此一个成熟的程序员在动手改本地代码之前，一定会先检查下远程库跟本地代码的区别！如果本地的代码版本已经落后，切记要先 pull 拉取一下远程库的代码，将本地

代码更新到最新以后，然后再修改，提交，推送！ 

#### 步骤

1、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052015950.png" alt="image-20220417170338395" style="zoom:50%;" />

2、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052015187.png" alt="image-20220417170551128" style="zoom:50%;" />



### clone到本地库

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052015252.png" alt="image-20220418154927579" style="zoom: 67%;" />



<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052015688.png" alt="image-20220418155021687" style="zoom:67%;" />





## gitee

### 新建仓库

1、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052015822.png" alt="image-20220418161605435" style="zoom:67%;" />

2、

设置仓库名称

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052015414.png" alt="image-20220418161637998" style="zoom:67%;" />

3、修改仓库状态

1、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052015916.png" alt="image-20220418161912760" style="zoom:67%;" />

2、

<img src="C:\Users\zsq\AppData\Roaming\Typora\typora-user-images\image-20220418162002121.png" alt="image-20220418162002121" style="zoom:67%;" />

3、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052015008.png" alt="image-20220418162130586" style="zoom:67%;" />



### 删除仓库

1、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052016703.png" alt="image-20220418162232228" style="zoom:67%;" />

2、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052016392.png" alt="image-20220418162304762" style="zoom:67%;" />

3、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052016305.png" alt="image-20220418162340931" style="zoom:67%;" />

4、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052016686.png" alt="image-20220418162426774" style="zoom:67%;" />

5、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052016601.png" alt="image-20220418162527770" style="zoom:67%;" />

6、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052016096.png" alt="image-20220418162615593" style="zoom:67%;" />





## idea集成Gitee

### push

1、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052016536.png" alt="image-20220418165930063" style="zoom:67%;" />

2、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052016587.png" alt="image-20220418170232958" style="zoom:67%;" />



### pull

1、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052017266.png" alt="image-20220418171153967" style="zoom:67%;" />

2、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052017260.png" alt="image-20220418172451289" style="zoom:67%;" />



## 码云赋值GitHab项目

### 步骤

1、在码云上新建仓库

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052017825.png" alt="image-20220418173124926" style="zoom:67%;" />

2、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052017795.png" alt="image-20220418173159783" style="zoom:67%;" />

3、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052017149.png" alt="image-20220418173414965" style="zoom:67%;" />

4、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052017570.png" alt="image-20220418173501522" style="zoom: 67%;" />

5、

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052017596.png" alt="image-20220418173814280" style="zoom:67%;" />

### 更新

<img src="https://gitee.com/js199000124/photo/raw/master/%20images/202205052017275.png" alt="image-20220418174127800" style="zoom:67%;" />

