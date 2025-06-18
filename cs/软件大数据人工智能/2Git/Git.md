项目中使用git构建分支流四种方式：	https://www.cnblogs.com/quartz/p/12814064.html

教程：https://www.liaoxuefeng.com/wiki/896043488029600/900388704535136



# 安装

### Git

https://zhuanlan.zhihu.com/p/242540359



### GUI

https://zhuanlan.zhihu.com/p/666417763





# 概念

![1543302039138](https://raw.githubusercontent.com/zhanghongyang42/images/main/1543302039138.png)



### 本地仓库

本地仓库：狭义的本地仓库特指版本库

​					广义的本地仓库包括 版本库，工作区，暂存区。



版本库（）：.git文件夹。这里的版本就是一个点，可以认为你每次commit都是一个版本。里面包括暂存区，master分支，指针HEAD

工作区：包含.git文件夹的目录，即可视的文件都位于工作区

暂存区：工作区到版本库的一个缓冲区域，位于.git中，工作区多次add到暂存区



创建本地仓库

git bash   ：     git   init



### 忽略文件

忽略文件不保存到版本库

在Git工作区的根目录下创建一个特殊的.gitignore文件，然后把要忽略的文件名填进去

```
*.a
!lib.a
/TODO
build/
```



# 文件保存

**工作区文件**

将文件放到工作区即可



**工作区添加暂存区**

git add readme.txt



**暂存区提交本地仓库**

git commit -m “注释”



**查看状态**

git status



# 分支操作

1. 并行开发：使用分支可以让团队成员同时在不同的分支上开发功能或修复bug，而不会相互干扰或影响彼此的工作。
2. 功能开发：分支可以用于开发新功能。当一个新功能需要多次提交才能完成时，使用分支可以保持主分支的代码稳定，而新功能开发不会影响其他人的工作。
3. 代码审查：使用分支，可以让其他团队成员更容易地审查你的更改。他们可以查看你的分支，并在合并到主分支之前提出建议或要求进行修改。
4. 版本发布：分支可以用于管理软件的版本发布。例如，创建一个单独的分支来发布稳定版本。新功能开发可以继续在主分支上进行开发。
5. 修复bug：当代码中出现问题时，你可以创建一个分支来修复bug，而不会影响主分支的稳定性。修复完成后，可以将修复的代码合并回主分支。



1. 查看分支：

   ```
   git branch
   ```

   此命令会显示所有本地分支，当前活动分支前会有一个星号(*)。

   

2. 创建分支：

   ```
   git branch <branch-name>
   ```

   使用此命令可以创建一个新分支，其中`<branch-name>`是你要创建的分支名称。

   

3. 切换分支：

   ```
   git checkout <branch-name>
   ```

   此命令用于切换到指定的分支，其中`<branch-name>`是你要切换到的分支名称。

   切换分支，就是切换仓库。

   切换分支或者新建并切换分支时，工作区未保存的更改内容将会丢失，所以切换分支时，要将工作区的内容保存后再切换。

   切换分支时，暂存区的内容不会变化，可以提交到新分支，但是不建议这样做，也要清理好暂存区再切换分支。

   

4. 创建并切换到新分支：

   ```
   git checkout -b <branch-name>
   ```

   此命令将创建一个新分支并立即切换到该分支，其中`<branch-name>`是你要创建的分支名称。

   

5. 删除分支：

   ```
   git branch -d <branch-name>
   ```

   删除指定的分支，分支的所有commit都已经合并到当前分支或者丢弃后才能成功删除。如果存在未合并的更改，需要使用`-D`选项来强制删除。

   

6. 合并分支：

   ```
   git merge <branch-name>
   ```

   此命令将指定分支的更改合并到当前分支，其中`<branch-name>`是你要合并的分支名称。

   分支冲突时，手动解决分支冲突再合并。

   

7. 重命名分支：

   ```
   git branch -m <old-branch-name> <new-branch-name>使用此命令可以重命名分支，将`<old-branch-name>`重命名为`<new-branch-name>`。
   ```

   

8. 查看所有分支（本地和远程）：

   ```
   git branch -a
   ```

   此命令会显示所有本地和远程分支。



# 工作区暂存

工作到一半，需要切换到其他分支工作，但是还不想commit即可暂存



1.暂存

git bash   ：     git stash

暂存后即可切换分支，保存工作区未提交内容，不会删除工作区内容



2.查看

git bash   ：     git stash list



3.恢复

git bash   ：     git stash pop



# 版本回退

### 工作区修改回退

工作区回退到版本库版本：做了修改，还没add，回到版本初始状态。

git checkout --文件名称



工作区回退到暂存区版本：add到暂存区了，又做了修改，想恢复暂存区文件。

git checkout --文件名称



### 暂存区修改回退

清空暂存区某些文件

git reset HEAD file



### 版本回退

版本库会维护所有commit过的版本，版本回退，会同时改变 暂存区+工作区。



查看所有分支的操作记录

```
git reflog 
```



查看当前分支所有commit记录

```
git log –pretty=oneline
```



回退到指定版本号

```
git reset --hard 版本号 
```



# -----------------------



# 远程仓库

可以自建远程仓库服务器，也可以使用github，gitlab等远程仓库。

一般的远程仓库提供ssh和http两种方式连接交互，ssh需要生成ssh密钥，http需要账号密码。



为了避免分支冲突，一定要先pull，确认没有冲突，再push。



1. 查看远程仓库：

   ```
   git remote -v
   ```

   此命令会显示所有远程仓库及其对应的URL。

   

2. 删除远程仓库：

   ```
   git remote rm <remote-name>
   ```

   使用此命令可以删除一个远程仓库，其中`<remote-name>`是你要删除的远程仓库名称。

   

3. 添加远程仓库：

   ```
   git remote add <remote-name> <remote-url>
   git remote add origin https://github.com/zhanghongyang42/远程仓库名.git
   ```

   使用此命令添加一个新的远程仓库，其中`<remote-name>`是远程仓库的名称（通常为origin），`<remote-url>`是远程仓库的URL。

   适用于本地已经有仓库，建一个远程空仓库，然后将本地仓库和远程仓库关联。

   

4. 克隆远程仓库：

   ```
   git clone <remote-url>
   git clone https://github.com/zhanghongyang42/远程仓库名
   ```

   使用此命令可以将远程仓库克隆到本地计算机，其中`<remote-url>`是远程仓库的URL。

   这种方法，本地要有远程的账号密码或者ssh公钥才能使用。ssh公钥配置暂时省略。

   ```
   需要的时候要输入 gitlab或者github的账户名和密码
   
   清除gitlab或者github的账户名和密码
   git credential-manager uninstall
   
   永久记住密码
   git config credential.helper store
   ```

   

5. 拉取远程仓库的变更并合并到当前分支：

   ```
   git pull <remote-name> <remote-branch-name>
   ```

   使用此命令可以从远程仓库拉取最新的更改，并将其合并到当前分支。

   `git pull`：该命令实际上是 `git fetch` 和 `git merge` 的组合。它会从远程仓库获取最新更改，并自动将这些更改合并到当前分支

   

6. 推送本地分支到远程仓库：

   ```
   git push <remote-name> <branch-name>
   ```

   将指定的本地分支推送到远程仓库，其中`<remote-name>`是远程仓库的名称（通常为origin），`<branch-name>`是你要推送的本地分支名称。



# 分支映射

1. 查看远程分支：

   ```
   git branch -r
   ```

   此命令会显示所有远程分支。

   

2. 查看映射关系

   ```
   git branch -vv
   ```

   

3. 设置本地分支跟踪远程分支：

   ```
   git branch --set-upstream-to=<remote-name>/<remote-branch-name> <local-branch-name>
   ```

   此命令将指定的本地分支与远程分支关联，以便在执行`git pull`和`git push`时自动同步。

   

4. 取消本地分支的跟踪远程分支：

   ```
   git branch --unset-upstream <local-branch-name>
   ```

   使用此命令可以取消指定本地分支对远程分支的跟踪。`<local-branch-name>`是你要取消跟踪的本地分支名称。



- 快捷命令：创建一个和远程分支相同本地分支，并跟踪远程分支：

  ```
  git checkout --track <remote-name>/<remote-branch-name>
  ```

  使用此命令可以将本地分支与远程分支关联起来，实现跟踪。

  

- 快捷命令：创建一个和本地分支相同远程分支，并跟踪远程分支：

  推送本地分支到远程仓库并设置跟踪关系：

  ```
  git push -u <remote-name> <local-branch-name>
  ```

  使用此命令可以将本地分支推送到远程仓库，并设置本地分支与远程分支的跟踪关系。

  

- 快捷命令：创建一个和远程分支相同本地分支，但是不会跟踪远程分支：

  ```
  git checkout -b <local-branch-name> <remote-name>/<remote-branch-name>
  git checkout -b my-feature origin/master
  ```



# -----------------------



# IDEA集成

### 集成Git和远程仓库

安装好IntelliJ IDEA后，如果Git安装在默认路径下，那么idea会自动找到git的位置，如果更改了Git的安装位置则需要手动配置下Git的路径。

选择File→Settings打开设置窗口，找到Version Control下的git选项：

![1543399359546](https://raw.githubusercontent.com/zhanghongyang42/images/main/1543399359546.png)

选择git的安装目录后可以点击“Test”按钮测试是否正确配置。

![1543399391526](https://raw.githubusercontent.com/zhanghongyang42/images/main/1543399391526.png)

![1550563988719](https://raw.githubusercontent.com/zhanghongyang42/images/main/1550563988719.png)



### 创建本地仓库

https://juejin.cn/post/7303804980342325285



### 从远程仓库克隆

​	关闭工程后，在idea的欢迎页上有“Check out from version control”下拉框，选择git

![1543401467964](https://raw.githubusercontent.com/zhanghongyang42/images/main/1543401467964.png)

![1543401508478](https://raw.githubusercontent.com/zhanghongyang42/images/main/1543401508478.png)



![1543401651635](https://raw.githubusercontent.com/zhanghongyang42/images/main/1543401651635.png)

> 使用idea选择克隆后, 会出现如下内容, 一![1543401862519](https://raw.githubusercontent.com/zhanghongyang42/images/main/1543401862519.png)直下一步即可





# Github使用

- 在GitHub上，可以任意Fork开源仓库；
- 自己拥有Fork后的仓库的读写权限；
- 可以clone，然后修改Fork后的仓库，然后push修改
- 可以把自己修改过的Fork后的仓库 pull request给官方仓库来贡献代码。





































