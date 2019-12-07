## 版本创建

**要想让git管理代码**

1.创建一个文件夹  **mkdir test**

2.进入创建的文件**cd test**

3.初始化仓库得到一个（.git）的 隐藏文件夹（这个目录下的代码都要靠生成的.git来管理）**git init** 

4.创建一个文件 **vi code.txt**  查看创建的文件 cat code.txt

5.创建一个版本（两步）

​	a.git add code.txt

​	b.git commit -m ' 版本名称 '

​	c.使用**git log**查看版本

# 版本回退

1.git log 查看版本

2.git reset --hard head^(回退到一个上一个版本)

2.git reset --hard 版本号（ 05a38ce8）

2.git reset --hard head~n（n代表数字，第几个就表示回到上几个版本）

3.git reflog (查看之前的版本操作，用于找回hard后消失的版本)



# 撤销修改

**撤销工作区的修改**

查看工作区的状态： git status

使用：git checkout -- 文件名   **撤销修改**

**如果文件在暂存区**

1.先退出暂存区状态   **git reset head 文件名**  （撤销暂存）  （git status 查看文件的状态）

2.git checkout -- 文件名

**以及创建了版本**

进行版本回退

# 对比文件有什么不同

**对比工作区与版本里的文件有什么不同**：git diff head -- 文件名

---代表版本里的

+++代表工作区的

前面没+没-的代表相同的



**比较两个版本之间有什么不同**

git diff head head~1 -- 文件名

---代表前面一个head

+++代表后面一个head



# 删除文件

rm 文件名

取消删除：git checkout -- 文件名  （撤销删除操作就行啦）

确定要删除：git rm 文件名



# 基础操作小结

工作区-------》暂存区-------》版本库

编辑文件都是在工作区

git add --文件名       |||将**工作区**的文件放入**暂存区**

git commit -m '版本名' ||| 将暂存区的修改一次性提交到版本记录中

# git分支

查看分支：git branch

创建分支：git branch <name>

切换分支：git checkout <name>   （head指针直接切换）

创建并切换分支：git checkout -b <name>

合并分支到当前分支：git merge <name>

删除分支：git branch -d <name>

两个模式：

​	1.Fast-forward（快速合并模式《直接移动指针》）

**当两个分支都提交了版本时快速合并会起冲突**

​	（两个分支都修改同一个文件并且都有新的提交）

​	**起冲突并且报错**

​	（两个分支修改不同的文件并且都有新的提交）

​	**起冲突但是不报错（会导致分支的数据消失）**

**解决办法：**

​	1.git status 查看时那个文件冲突

​	2.vi 文件名 进入文件修改冲突

​	3.git add 文件名   重新提交

​	4.git commit -m ' 说明 '  

**查看分支冲突：**

​	git log --graph --pretty=oneline

**禁用Fast-forward：** 

​	git merge --no-ff -m '备注'

# bug分支

遇到要修复的紧急bug时，可能需要先放下手头的工作区修复bug，但是这时候你手头的工作还没有完成，不能提交，这时候就应该先将手头的工作存起来，

使用：git stash （git会将当前的工作先暂存起来）

然后创建一个新的临时的bug分支取修复bug，修复完后提交，然后回到主分支取合并，并将临时分支删除

最好是**禁用快速合并**，否者当你将bug分支删除后你看不到bug修改记录

（git log --graph --pretty=oneline）

当你修复完bug后需要继续编辑时，

使用：git stash list (会列出你保存的工作现场)

然后使用 git stash pop （就可以恢复工作现场）

 # github

1.创建一个仓库

2.在setting中设置一下ssh公钥

3.获取本机的公钥 

​	**a.直接cd到母目录**

​	**b.vi .gitconfig 在里面的name和email中填写自己的github名称和邮箱**

​	**c.ssh-keygen -t rsa -C '邮箱号' 然后一直回车 会生成两个重要的文件**

​	（注意ssh-keygen之间不能有空格）

**（id_rsa 和 id_rsa.pub）id_rsa是自己需要保留的 id_rsa.pub是贴到setting里面的ssh公钥**

​	**d.cd .ssh**

​	**e.ls**

​	**f.cat id_rsa.pub**

​	**g.复制ssh公钥到github上**

### 从git中克隆

1.github仓库里选择克隆的地址

2.git clone <克隆地址>

3.ls查看文件

**如果出现错误：**

​	执行：1.eval "$(ssh-agent  -s)"

​		   2.ssh-add

**开发时一般都不在master分支上开发而是从新创建一个分支**

### 推送分支

1.关联远程仓库     git remote add origin 远程仓库地址

2.提交分支       git push origin 分支姓名

（第一次提交由于仓库里没有数据所有需要在push后加上-u）

### 跟踪远程分支

git branch --set-upstream-to=origin/远程分支名   本地分支名

本地分支跟踪远程分支

### 从远程分支拉取代码

git pull origin 分支名称