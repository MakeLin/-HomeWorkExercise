#### git

- 首次安装git必须设置一下用户签名，否则无法提交文件。签名主要是用来区分操作者的，用户的签名在每一个版本的提交信息中都能看到，用来确认本次提交是谁的。
  - 💎签名与用来登录GitHub、gitee码云等托管中心的账号没有关系，只是在本地库中起作用的。

```
## 配置签名信息
$git config --global user.name ck
$git config --global user.email ck@outlook.com
```

- 初始化本地库

  - 初始化本地库的目的可以理解为就是让git拥有这个目录的管理权限

  ```
  ## 初始化本地库
  ## 进入项目所在目录下执行下面的命令
  $git init
  ## 执行成功后将会在当前目录下产生一个.git文件夹					
  ```

  - 查看本地库状态

  ```
  git status
  ```

- git 管理命令

```
## 将文件从工作区添加到暂存区
$git add <file>

## 将文件从暂存区删除
## 不会删除工作区文件
## <file> 表示此处需要填写一个文件名，...此处可以添加多个文件名，并不是真的要在真正写的命令末尾加上三个点
$git rm --cached <file>...  

## 将文件提交到本地库
## -m选项用来指定文件提交信息，
## 如果由多个-m选项，他们会被连接成一个段落
$git commit [-F <file> | -m <msg>]
## 随意点的写法
$git commit [-m <msg>] <file>
##最好把-m选项写上，因为如果不写这个选项，他将会在你提交这个命令后，打开一个新的窗口，让你填写提交信息。

## 查看项目的版本信息
## git reflog
## git log
## reflog 显示的信息简洁一点（版本号也很简洁）
## log 会显示全部版本信息（包括签名信息）

```



- git使用过程中文件的所在位置

```
## 最开始：			工作区（还未被git工具管理，尚未git add）
## git add后：  	 暂存区（已添加到git中，还未上传到本地库，此时删除还来得及）
## git commit后：	 本地库（提交成功后，将会形成历史版本信息，此时删不掉的，除非删除本地库）

```



- git回滚历史版本

```
##回滚
git reset --hard 版本号

```

- git分支

  ```
  在版本控制过程中，同时推进多个任务，为每个任务，我们就可以创建每个任务的单独分支。使用分支意味着程序员可以把自己的工作从开发主线上分离开来，开发自己分支的时候，不会影响主线分支的运行。对于初学者而言，分支可以简单理解为副本，一个分支就是一个单独的副本。（分支底层其实也是指针的引用）
  ```

  - git 分支操作

  ```
  ## git查看分支
  $git branch -v
  
  ## git创建分支
  $git branch <branch>
  
  ## git切换分支
  $git checkout <branch>
  
  ## git合并分支
  $git merge <branch>
  
  ## 分支合并产生冲突时，需打开要合并的文件进行手动合并
  ## <<<<<<<< HEAD
  ## ....		这中间的内容是`当前分支`中引起冲突的修改
  ## ========
  ## ....		这中间的内容是`anotherBranch`这个分支中引起冲突的修改
  ## >>>>>>>> anotherBranch
  ```

  

  - 什么时候进行分支合并，才会产生合并冲突？

  当两个分支中对同一个文件做了不同的修改时。如果一个分支对这个文件没有进行修改，那么合并的时候就不会引起合并冲突。

  - 合并失败后，如何手动合并?

  在当前分支中，打开发生冲突的文件将想保留的代码保留下来（💎把其余的都删掉，包括用来标记冲突的特殊符号）

  然后，git add `<file>`，之后执行git commit 。（💎最后执行的git commit 后边不要再跟文件名，否则会失败。）

  最后，顺利的话手动合并完成。（💎被合并的分支中的内容没有被同步修改，仍然保留着合并前的代码。）

  

- 团队内协作

  - 

- 跨团队协作

  -  

#### GitHub

- git查看远程库

  🐴 git remote -v

- git给远程库起别名

  🐴git remote add `<alias-name>` `<URL>`	

- git向远程库推送

  🐴git push `<remote-repository>`  `<branch>`

- git拉取远程库

  🐴git poll `<remote-repository>` `<branch>`

  💎拉取远程库后，它会自动提交本地库，不需要人为git commit更新本地库。

- git 克隆远程库

  🐴git clone `<URL>`

  💎clone会完成的操作：1.拉取代码 2.初始化本地库 3.给克隆的远程库添加别名

- SSH免密登录

  - 在自己的家目录下鼠标右键选择Git Bash Here(🌰家目录:c:/用户/ck, ck是我的Windows当前登录用户 )

  - 🐴ssh-keygen -t rsa -C 9185853@qq.com 

    💎-t 即type 用来指定加密协议 -C 用来指定目标用户

- git配置忽略文件（💎简单地说，就是我们只关心pom.xml和src下的源码，其他的我们都不要）

  `尚硅谷——如何设置忽略文件：`

  1）创建忽略规则文件 xxxx.ignore（前缀名随便起，建议是 git.ignore） 这个文件的存放位置原则上在哪里都可以，为了便于让~/.gitconfig 文件引用，建议也放在用 户家目录下 git.ignore 文件模版内容如下：

  ```
  # Compiled class file 
  *.class   
  # Log file 
  *.log 
  # BlueJ files
  *.ctxt 
  # Mobile Tools for Java (J2ME)
  .mtj.tmp/ 
  # Package Files 
  #
  *.jar 
  *.war 
  *.nar 
  *.ear 
  *.zip 
  *.tar.gz 
  *.rar 
  # virtual machine crash logs
  hs_err_pid* 
  .classpath 
  .project 
  .settings 
  target 
  .idea 
  *.iml 
  ```

   2）在.gitconfig 文件中引用忽略配置文件（此文件在 Windows 的家目录中） [user] name = Layne email = Layne@atguigu.com [core] excludesfile = C:/Users/asus/git.ignore 注意：这里要使用“正斜线（/）”，不要使用“反斜线（\）

  

#### gitee

#### gitLab