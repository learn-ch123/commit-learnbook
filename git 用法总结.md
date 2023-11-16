# 一、安装git

## 下载地址：

https://git-scm.com/downloads

###### 安装后测试：

```git
//输入本机的姓名和邮箱
git config --global user.name "Your Name"
git config --global user.email "2378068036@example.com"
```

![image-20231115085932554](https://gitee.com/chen-hao111222/images/raw/master/img/202311150859595.png)

# 二：创建仓库

```
mkdir [库名]
cd [库名]
pwd //显示一下所处位置

//把仓库变成可以管理的
git init	//在一个目录下输入命令，该命令就会变成一个git仓库
```

```
git init [指定目录]		//初始化仓库
```

![image-20231115084950314](https://gitee.com/chen-hao111222/images/raw/master/img/202311150849354.png)

```
vi learn.txt
git add learn.txt
git commit -m "提交备注或描述"
```

![image-20231115085429168](https://gitee.com/chen-hao111222/images/raw/master/img/202311150854213.png)



###### 拷贝项目

```
git clone git@github.com/learn-ch123/cc1

```

![image-20231115085607964](https://gitee.com/chen-hao111222/images/raw/master/img/202311150856995.png)

# 三：连接远程

## **生成SSH Key密钥**

**这个命令没运行一次就会生成一个新的密钥，就要去GitHub中SSH KEY中修改**

![image-20231114232517074](https://gitee.com/chen-hao111222/images/raw/master/img/202311142325113.png)

![image-20231114232544197](https://gitee.com/chen-hao111222/images/raw/master/img/202311142325237.png)

### 密钥

![image-20231114232624487](https://gitee.com/chen-hao111222/images/raw/master/img/202311142326524.png)

### 配置GitHub密钥

登陆GitHub，打开“Account settings”，“SSH Keys”页面：

![image-20231114232649622](https://gitee.com/chen-hao111222/images/raw/master/img/202311142326657.png)

然后，点“Add SSH Key”

![image-20231114232714862](https://gitee.com/chen-hao111222/images/raw/master/img/202311142327910.png)

点击 New SSH key (新建 ssh 密钥)

![image-20231114232739598](https://gitee.com/chen-hao111222/images/raw/master/img/202311142327634.png)

在Key文本框里粘贴`id_rsa.pub`文件的内容：填上任意Title

![image-20231114232759686](https://gitee.com/chen-hao111222/images/raw/master/img/202311142327730.png)

在GitHub中创建一个仓库，name,Description任意，记住仓库名

![image-20231114232833278](https://gitee.com/chen-hao111222/images/raw/master/img/202311142328326.png)

**复制远程仓库的ssh地址，只出现一次**

![image-20231114232853630](https://gitee.com/chen-hao111222/images/raw/master/img/202311142328670.png)

### 本地连接远程仓库

```
mkdir chen
cd chen
pwd
git init
//生成连接的SSH KEY
ssh-keygen -t rsa -C "2378068036@qq.com"	//最好不要更改，输入一次就改一次
cat ~/.ssh/id_rsa.pub		//复制到ssh里面

//连接GitHub的仓库
git remote add [本地remote名] git@github.com:[账号名]/[仓库名.git] [指定存储本地项目名]
git remote		//查看本地仓库别名
git remote -v

//测试连接是否成功--看下图就可以了
ssh -T git@github.com

//在GitHub中搞好ssh之后就可以弄了
//下载到本机
git clone git@github.com:learn-ch123/cc1.git

ls
cd cc1		//进去
vi 文件名		//可以add和commit后发送到GitHub
cat 文件名
git add 文件名
git commit -m "备注"
git log		//查看改动
git checkout -b dev		//建立一个新分支，把main分支复制到这里
git merge main			//复制到dev中
git push origin dev		//把新建的分支提交到GitHub中
```

###### clone

```
git remote add [本地remote名] git@github.com:learn-ch123/线上仓库名.git [指定本地目录]
```

![image-20231115090856888](https://gitee.com/chen-hao111222/images/raw/master/img/202311150908915.png)

指定下载到本地目录

![image-20231115092240423](https://gitee.com/chen-hao111222/images/raw/master/img/202311150922460.png)

# 四：基本操作

## 添加提交删除

```
git add [文件名]
git commit -m "备注"
```

```
//删除
git rm [文件名]	//删除工作区文件，并将这次删除放入暂存区
git rm --cached [文件名]	//停止追踪该文件，但是会保留在该工作区
```

```
//添加
git add [目录]		//添加目录
git add git add .	//对于多个变化一起提交
git add -p	//同文件中有多个变化，每次提交变化都会要求确定，可以实现分次提交
```

```
//提交
git commit -m [message]		//提交，添加备注信息
git commit [文件1] [文件2]	-m [message]	//提交指定文件到仓库
git commit -a 	//提交从上传提交到现在的所有变化
git commit -v	//提交后显示所有diff信息
```

## 查看状态

```
git status	//查看仓库当前的状态，显示有变更的文件
```

![image-20231115093014372](https://gitee.com/chen-hao111222/images/raw/master/img/202311150930413.png)

## 查看差异

```
git diff
git diff HEAD 版本号		//查看两个版本间的区别
git diff HEAD -- [文件名]	//查看一个文件工作区和仓库中的区别

//显示两个提交之间的差异
gitt diff [第一分支] [第二分支]

//显示某次提交的原数据和内容的变化
git show [提交名前四个数值]

//显示某次提交发生变化的文件
git show --name-only [commit]

//显示某次提交时，某个文件的内容
git show [commit]:[文件名]
```

<img src="https://gitee.com/chen-hao111222/images/raw/master/img/202311161603046.png" alt="image-20231115161943989"  />

## 查看版本

```
git log		//显示每次提交的版本信息和变更信息
git reflog 	//记录修改版本的历史

//显示某个提交之后的所有变动，每个提交占一行
git log [tag] HEAD --pretty=format:%s

//显示过去的5次提交
git log -5 --pretty --oneline

//显示所有提交过的用户，按照提交次数排序
git shortlog -sn

//显示某个文件是什么人什么时间修改过
git blame [文件名]
```



## 远程操作

###### remote

```
//创建一个新的本地remote
 git remote add [本地remote名] git@github.com:learn-ch123/learngit.git
 //查看所有远程库
 git remote -v
 
 //删除远程库
 git rmote rm [remote]
```

<img src="https://gitee.com/chen-hao111222/images/raw/master/img/202311161603464.png" alt="image-20231115203924753"  />

<img src="https://gitee.com/chen-hao111222/images/raw/master/img/202311161603152.png" alt="image-20231115203938237"  />

```
//显示某个远程库的信息
git remote show [远程库remote]
```

<img src="https://gitee.com/chen-hao111222/images/raw/master/img/202311161603759.png" alt="image-20231115204610288"  />

###### fetch

```
//下载远程仓库的变动，需要有变动才会有反应
git fetch [远程remote]
//注意远程的remote：git@github.com:learn-ch123/learngit.git	要全部的路径
```

<img src="https://gitee.com/chen-hao111222/images/raw/master/img/202311161603034.png" alt="image-20231115202355448"  />

###### pull

```
//取回远程仓库的变化和本地分支合并
git pull [远程remote] [本地branch]
//注意远程的remote：git@github.com:learn-ch123/learngit.git	要全部的路径
```

![image-20231115202526565](https://gitee.com/chen-hao111222/images/raw/master/img/202311152025615.png)

###### push

```
//第一次提交本地的分支的更新到远程库
//需要有一个新东西添加和提交之后才能push
//一定要在被提交的本地分支下push
git push -u [远程remote] [远程分支名]

//强行推送当前分支到远程库的某个分支，即使有冲突
git push [远程remote] --force

//推送所有分支到远程库
git push [远程remote] --all

//删除远程分支或标签--未实验
git push [remote] :[branch or tag]
```

<img src="https://gitee.com/chen-hao111222/images/raw/master/img/202311161603507.png" alt="image-20231115205118405"  />

## 撤销回退版本reset

```
//撤销工作目录中所有未提交的文件中修改的内容
git reset --hard HEAD

//撤销指定文件中未提交的修改内容
git checkout HEAD [文件名]
```

<img src="https://gitee.com/chen-hao111222/images/raw/master/img/202311161603081.png" alt="image-20231115210900835"  />

```
//撤销指定的提交版本
git reset [commit前四个值]

//当需要回到没更改前的版本方法
git reflog		//看一下更改前的版本号
git reset [commit]

//回退到之前1天的版本
git log --before="1 days"

//重置add过的指定文件和上一次commit的保持一致，但是工作区的不变
git reset [文件名]
//重置当前分支，当工作区的不变
git reset [commit]

//重置add和工作区，和上次commit的一致
git reset --hard
//重置当前分支所有内容，和指定commit的一致
git reset --hard[commit]
//重置当前分支，当add和工作区不变
git reset --keep [commit]
```



## 暂存stash

当你在某个分支的工作区中编写文件，在还没有完成（不想提交）的时候需要到另外一个分支工作，则需要把他储存起来，然后过段时间再回来操作

```
git stash 	//把正在改变的存储在一个地方

//查看之前工作现场都放到哪里去了
git stash list

//恢复工作现场，但是stash内容不删除
git stash apply

//恢复工作现场，并删除stash中内容
git stash pop
```

![image-20231115225042982](https://gitee.com/chen-hao111222/images/raw/master/img/202311152250033.png)



# 五：配置别名

```
//把一些较长的命令简写
git config --global alias.co checkout

commit--cm
checkout--co
branch--br
git@github.com:learn-ch123--gg

//对当前用户起作用
加上--global	//不加则针对当前的仓库起作用

//git配置文件放在.git/config中
cat .gitconfig		//需要在主目录中查看
```

![image-20231116093604235](https://gitee.com/chen-hao111222/images/raw/master/img/202311160936406.png)

## 本地仓库的remote查看

![image-20231116093727759](https://gitee.com/chen-hao111222/images/raw/master/img/202311160937890.png)

# 六：创建标签

切换到需要打标签的分支上

```
git branch		//查看所有分支
git switch [branch]		//切换标签
git tag v1.0	//为这个分支打上标签
git tag v2.0 [commit]		//为这个分支的某次提交打上标签
git tag			//查看分支所有标签
git tag -a v3.0 -m "备注" [commit]	//为标签打上备注
git show [tagname]		//查看标签的备注
```

<img src="https://gitee.com/chen-hao111222/images/raw/master/img/202311160945874.png" alt="image-20231116094547812" style="zoom:150%;" />

<img src="https://gitee.com/chen-hao111222/images/raw/master/img/202311160946050.png" alt="image-20231116094640895" style="zoom:150%;" />

![image-20231116094753776](https://gitee.com/chen-hao111222/images/raw/master/img/202311160947920.png)

```
git tag -d v1.0		//删除v0.1的标签
git push [远程remote] v1.0		//把本分支v1.0版本提交到远程仓库
git push [远程remote] --tags		//一次性提交全部尚未推送的本地标签
```

<img src="https://gitee.com/chen-hao111222/images/raw/master/img/202311160948092.png" alt="image-20231116094848986" style="zoom:150%;" />

<img src="https://gitee.com/chen-hao111222/images/raw/master/img/202311160959302.png" alt="image-20231116095931197" style="zoom:150%;" />

<img src="https://gitee.com/chen-hao111222/images/raw/master/img/202311161000358.png" alt="image-20231116100019274" style="zoom:150%;" />

```
//删除已经推送到了远程仓库的标签，先删除本地的
git tag -d v1.0		//删除本地标签
git push [远程remote] :目录/分支/标签
```

![image-20231116100236939](https://gitee.com/chen-hao111222/images/raw/master/img/202311161002051.png)



# 七：暂存区返回工作区

如果你不小心把文件add了，但是还想改动的话，就要把他返回到工作区

```
//恢复暂存区的指定文件到工作区
git checkout [file]
//恢复所有暂存区的文件到工作区
git checkout .

//恢复某个已经提交的文件到暂存区和工作区
git checkout [commit] [file]
```



如果你在工作区中修改了文件，但是都是废话，想要删掉

```
git checkout -- [file]
```

![image-20231116154731714](https://gitee.com/chen-hao111222/images/raw/master/img/202311161553349.png)