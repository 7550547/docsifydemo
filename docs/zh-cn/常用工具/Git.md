## Git 工作区、暂存区和版本库
### 基本概念
我们先来理解下 Git 工作区、暂存区和版本库概念：

- 工作区：就是你在电脑里能看到的目录。

- 暂存区：英文叫 stage 或 index。一般存放在 .git 目录下的 index 文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。

- 版本库：工作区有一个隐藏目录 .git，这个不算工作区，而是 Git 的版本库。
  下面这个图展示了工作区、版本库中的暂存区和版本库之间的关系：

  ![img](https://www.runoob.com/wp-content/uploads/2015/02/1352126739_7909.jpg)
## 常用命令
### git clone 命令

执行远程操作的第一步，通常是从远程主机克隆一个版本库，这时就要用到`git clone`命令。

```shell
$ git clone <版本库的网址>
Shell
```

比如，克隆jQuery的版本库。

```shell
$ git clone http://github.com/jquery/jquery.git
Shell
```

`git clone`支持多种协议，除了HTTP(s)以外，还支持SSH、Git、本地文件协议等，下面是一些例子。

SSH协议还有另一种写法。

```shell
$ git clone [user@]example.com:path/to/repo.git
Shell
```

通常来说，Git协议下载速度最快，SSH协议用于需要用户认证的场合。

## git status命令

`git status`命令用于显示工作目录和暂存区的状态。使用此命令能看到那些修改被暂存到了, 哪些没有, 哪些文件没有被Git tracked到。`git status`不显示已经`commit`到项目历史中去的信息。看项目历史的信息要使用`git log`.

![image-20210220103552140](C:\Users\28345\AppData\Roaming\Typora\typora-user-images\image-20210220103552140.png)

红色代表在本地修改还没有提交到本地仓库，绿色代表提交到了本地仓库，还没有提交到远程仓库

## git add 命令

### 描述

此命令将要提交的文件的信息添加到索引库中(将修改添加到暂存区)，以准备为下一次提交分段的内容。 它通常将现有路径的当前内容作为一个整体添加，但是通过一些选项，它也可以用于添加内容，只对所应用的工作树文件进行一些更改，或删除工作树中不存在的路径了。

“索引”保存工作树内容的快照，并且将该快照作为下一个提交的内容。 因此，在对工作树进行任何更改之后，并且在运行`git commit`命令之前，必须使用`git add`命令将任何新的或修改的文件添加到索引。

该命令可以在提交之前多次执行。它只在运行`git add`命令时添加指定文件的内容; 如果希望随后的更改包含在下一个提交中，那么必须再次运行`git add`将新的内容添加到索引。

`git status`命令可用于获取哪些文件具有为下一次提交分段的更改的摘要。

默认情况下，`git add`命令不会添加忽略的文件。 如果在命令行上显式指定了任何忽略的文件，`git add`命令都将失败，并显示一个忽略的文件列表。由Git执行的目录递归或文件名遍历所导致的忽略文件将被默认忽略。 `git add`命令可以用`-f(force)`选项添加被忽略的文件。

### 示例

以下是一些示例 -

添加`documentation`目录及其子目录下所有`*.txt`文件的内容：

```shell
$ git add documentation/*.txt
Shell
```

> 注意，在这个例子中，星号`*`是从shell引用的; 这允许命令包含来自 `Documentation/`目录和子目录的文件。

```shell
$ git add .  # 将所有修改添加到暂存区
$ git add *  # Ant风格添加修改
$ git add *Controller   # 将以Controller结尾的文件的所有修改添加到暂存区

$ git add Hello*   # 将所有以Hello开头的文件的修改添加到暂存区 例如:HelloWorld.txt,Hello.java,HelloGit.txt ...

$ git add Hello?   # 将以Hello开头后面只有一位的文件的修改提交到暂存区 例如:Hello1.txt,HelloA.java 如果是HelloGit.txt或者Hello.java是不会被添加的
Shell
```
## git commit 命令
git commit 命令将暂存区内容添加到本地仓库中。

提交暂存区到本地仓库中:
```shell
git commit -m"message"

```
## git push origin 命令

### 描述

使用本地引用更新远程引用，同时发送完成给定引用所需的对象。可以在每次推入存储库时，通过在那里设置挂钩触发一些事件。

当命令行不指定使用`<repository>`参数推送的位置时，将查询当前分支的`branch.*.remote`配置以确定要在哪里推送。 如果配置丢失，则默认为`origin`。

### 示例

以下是一些示例 -

```shell
$ git push origin master
Shell
```

上面命令表示，将本地的`master`分支推送到`origin`主机的`master`分支。如果`master`不存在，则会被新建。

如果省略本地分支名，则表示删除指定的远程分支，因为这等同于推送一个空的本地分支到远程分支。

```shell
$ git push origin :master
# 等同于
$ git push origin --delete master
Shell
```

上面命令表示删除`origin`主机的`master`分支。如果当前分支与远程分支之间存在追踪关系，则本地分支和远程分支都可以省略。

```shell
$ git push origin
Shell
```

上面命令表示，将当前分支推送到`origin`主机的对应分支。如果当前分支只有一个追踪分支，那么主机名都可以省略。

```shell
$ git push
Shell
```

如果当前分支与多个主机存在追踪关系，则可以使用`-u`选项指定一个默认主机，这样后面就可以不加任何参数使用`git push`。

```shell
$ git push -u origin master
Shell
```

上面命令将本地的`master`分支推送到`origin`主机，同时指定`origin`为默认主机，后面就可以不加任何参数使用`git push`了。

不带任何参数的`git push`，默认只推送当前分支，这叫做`simple`方式。此外，还有一种`matching`方式，会推送所有有对应的远程分支的本地分支。Git 2.0版本之前，默认采用`matching`方法，现在改为默认采用`simple`方式。如果要修改这个设置，可以采用`git config`命令。

```shell
$ git config --global push.default matching
# 或者
$ git config --global push.default simple
Shell
```

还有一种情况，就是不管是否存在对应的远程分支，将本地的所有分支都推送到远程主机，这时需要使用`–all`选项。

```shell
$ git push --all origin
Shell
```

上面命令表示，将所有本地分支都推送到`origin`主机。
如果远程主机的版本比本地版本更新，推送时Git会报错，要求先在本地做`git pull`合并差异，然后再推送到远程主机。这时，如果你一定要推送，可以使用`–force`选项。

```shell
$ git push --force origin
Shell
```

上面命令使用`-–force`选项，结果导致在远程主机产生一个”非直进式”的合并(non-fast-forward merge)。除非你很确定要这样做，否则应该尽量避免使用`–-force`选项。

最后，`git push`不会推送标签(tag)，除非使用`–tags`选项。

```shell
$ git push origin --tags
Shell
```

将当前分支推送到远程的同名的简单方法，如下 - 

```shell
$ git push origin HEAD
Shell
```

将当前分支推送到源存储库中的远程引用匹配主机。 这种形式方便推送当前分支，而不考虑其本地名称。如下 - 

```shell
$ git push origin HEAD:master
```
## git分支管理

分支操作允许创建另一路线/方向上开发。我们可以使用这个操作将开发过程分为两个不同的方向。 例如，我们发布了`1.0`版本的产品，可能需要创建一个分支，以便将`2.0`功能的开发与`1.0`版本中错误修复分开。

## 创建分支

我们可使用`git branch <branch name>`命令创建一个新的分支。可以从现有的分支创建一个新的分支。 也可以使用特定的提交或标签作为起点创建分支。 如果没有提供任何特定的提交ID，那么将以`HEAD`作为起点来创建分支。参考如下代码，创建一个分支：*new_branch* - 

```shell
$ git branch new_branch

Administrator@MY-PC /D/worksp/sample (master)
$ git branch
* master
  new_branch
Shell
```

执行上命令后，它创建了一个新的分支：*new_branch*; 使用`git branch`命令列出可用的分支。Git在当前签出分支之前显示一个星号。

创建分支操作的图示表示如下：

![img](http://www.yiibai.com/uploads/images/201707/1007/523110754_88289.png)

![img](http://www.yiibai.com/uploads/images/201707/1107/893120729_65032.png)

## 切换分支

使用`git checkout`命令在分支之间切换。

```shell
$ git checkout new_branch
M       src/string.py
Switched to branch 'new_branch'
Shell
```

## 创建和切换分支的快捷方式

在上面的例子中，分别使用两个命令创建和切换分支。 Git为`checkout`命令提供`-b`选项; 此操作将创建一个新的分支，并立即切换到新分支。

```shell
$ git checkout -b test_branch
M       src/string.py
Switched to a new branch 'test_branch'

Administrator@MY-PC /D/worksp/sample (test_branch)
$ git branch
  master
  new_branch
* test_branch
Shell
```

## 删除分支

可以通过向`git branch`命令提供`-D`选项来删除分支。 但在删除现有分支之前，请切换到其他分支。

如上面所示，目前在`test_branch`分支，如要想删除该分支。需要先切换到其它分支再删除此分支，如下所示。

```shell
$ git branch
  master
  new_branch
* test_branch

Administrator@MY-PC /D/worksp/sample (test_branch)

$ git checkout master
M       src/string.py
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 4 commits.
  (use "git push" to publish your local commits)

Administrator@MY-PC /D/worksp/sample (master)

$ git branch -D test_branch
Deleted branch test_branch (was b759faf).
Administrator@MY-PC /D/worksp/sample (master)
Shell
```

当前剩下的分支如下 - 

```shell
$ git branch
* master
  new_branch
Shell
```

## 重命名分支

假设需要在项目中添加对宽字符的支持。并且已经创建了一个新的分支，但分支名称需要重新命名。那么可通过使用`-m`选项后跟旧的分支名称和新的分支名称来更改/重新命名分支名称。

```shell
$ git branch
* master
  new_branch

Administrator@MY-PC /D/worksp/sample (master)
$ git branch -m new_branch wchar_support
Shell
```

现在，使用`git branch`命令显示新的分支名称。

```shell
$ git branch
* master
  wchar_support
Shell
```

## 合并两个分支

实现一个函数来返回宽字符串的字符串长度。新的代码将显示如下：

```shell
$ git branch
master
* wchar_support

$ pwd
/D/worksp/sample

Administrator@MY-PC /D/worksp/sample (master)
$ git diff
diff --git a/src/string.py b/src/string.py
index 18f165f..89e82b3 100644
--- a/src/string.py
+++ b/src/string.py
@@ -8,3 +8,9 @@ print ("var2[1:5]: ", var2[1:5]) #   切片 加索引

 def my_strcat(str1, str2):
        return (str1+str2)
+
+a = '我'
+b = 'ab'
+ab = '我ab'
+
+print(len(a), len(b), len(ab), len('='))
\ No newline at end of file

Administrator@MY-PC /D/worksp/sample (master)
Shell
```

假设经过测试，代码没有问题，最后将其变更推送到新分行。

```shell
$ git status
On branch master
Your branch is ahead of 'origin/master' by 5 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   src/string.py

no changes added to commit (use "git add" and/or "git commit -a")

Administrator@MY-PC /D/worksp/sample (master)
$ git add src/string.py

Administrator@MY-PC /D/worksp/sample (master)
$ git commit -m 'Added w_strlen function to return string lenght of wchar_t
> string'
[master 6bab70a] Added w_strlen function to return string lenght of wchar_t string
 1 file changed, 6 insertions(+)
Shell
```

请注意，下面将把这些更改推送到新的分支，所以这里使用的分支名称为`wchar_support`而不是`master`分支。

执行过程及结果如下所示 - 

```shell
$ git push origin wchar_support
Username for 'http://git.oschina.net': 769728683@qq.com
Password for 'http://769728683@qq.com@git.oschina.net':
Counting objects: 18, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (12/12), done.
Writing objects: 100% (15/15), 1.72 KiB | 0 bytes/s, done.
Total 15 (delta 3), reused 0 (delta 0)
To http://git.oschina.net/yiibai/sample.git
 * [new branch]      wchar_support -> wchar_support

Administrator@MY-PC /D/worksp/sample (master)
Shell
```

提交更改后，新分支将显示如下：

![img](http://www.yiibai.com/uploads/images/201707/1107/852150706_30997.png)

如果其他开发人员很想知道，我们在私人分支上做什么，那么可从`wchar_support`分支检查日志。

```
yiibai@ubuntu:~/git/sample$ git log origin/wchar_support -2
```

输出结果如下 - 

```shell
yiibai@ubuntu:~/git/sample$ pwd
/home/yiibai/git/sample
yiibai@ubuntu:~/git/sample$ git pull
remote: Counting objects: 15, done.
remote: Compressing objects: 100% (12/12), done.
remote: Total 15 (delta 3), reused 0 (delta 0)
Unpacking objects: 100% (15/15), done.
From http://git.oschina.net/yiibai/sample
 * [new branch]      wchar_support -> origin/wchar_support
Already up-to-date.
yiibai@ubuntu:~/git/sample$ git log origin/wchar_support -2
commit b759fafeb2a58bd1104f4142e4c0ababdadce01d
Author: maxsu <your_email@mail.com>
Date:   Mon Jul 10 23:44:24 2017 +0800

    fdasjkfdlaks

commit de08fcc70df3a31c788a2e926263b18498d2df09
Author: maxsu <your_email@mail.com>
Date:   Mon Jul 10 23:40:00 2017 +0800

    delete
yiibai@ubuntu:~/git/sample$
Shell
```

通过查看提交消息，其他开发人员(`minsu`)到有一个宽字符的相关计算函数，他希望在`master`分支中也要有相同的功能。不用重新执行代码编写同样的代码，而是通过将分支与主分支合并来执行代码的合并。下面来看看应该怎么做？

```shell
yiibai@ubuntu:~/git/sample$ git branch
* master

yiibai@ubuntu:~/git/sample$ pwd
/home/yiibai/git/sample

yiibai@ubuntu:~/git/sample$ git merge origin/wchar_support
Updating 44ea8e4..b759faf
Fast-forward
 src/string.py | 4 +++-
 1 file changed, 3 insertions(+), 1 deletion(-)
yiibai@ubuntu:~/git/sample$
Shell
```

合并操作后，`master`分支显示如下：

![img](http://www.yiibai.com/uploads/images/201707/1107/436150723_30142.png)

现在，分支`wchar_support`已经和`master`分支合并了。 可以通过查看提交消息或者通过查看`string.py`文件中的修改来验证它。

```shell
yiibai@ubuntu:~/git/sample$ git branch
* master
yiibai@ubuntu:~/git/sample$ cd src/
yiibai@ubuntu:~/git/sample/src$ git log -2
commit b759fafeb2a58bd1104f4142e4c0ababdadce01d
Author: maxsu <your_email@mail.com>
Date:   Mon Jul 10 23:44:24 2017 +0800

    fdasjkfdlaks

commit de08fcc70df3a31c788a2e926263b18498d2df09
Author: maxsu <your_email@mail.com>
Date:   Mon Jul 10 23:40:00 2017 +0800
Shell
```

上述命令将产生以下结果。

```python
#!/usr/bin/python3

var1 = 'Hello World!'
var2 = "Python Programming"

print ("var1[0]: ", var1[0])
print ("var2[1:5]: ", var2[1:5]) #   切片 加索引

def my_strcat(str1, str2):
    return (str1+str2)

a = '我'
b = 'ab'
ab = '我ab'

print(len(a), len(b), len(ab), len('='))
Python
```

测试后，就可将代码更改推送到`master`分支了。

```shell
$ git push origin master
Total 0 (delta 0), reused 0 (delta 0)
To http://git.oschina.net/yiibai/sample.git
5776472..64192f9 master −> master
```



---

## Git 使用教程

- [学习 git 分支-可视化学习，超赞 👍](https://learngitbranching.js.org/?demo=&locale=zh_CN)
- [图解 Git](http://marklodato.github.io/visual-git-guide/index-zh-cn.html)
- [Think like a Git](http://think-like-a-git.net/)
- [Git教程 廖雪峰](https://www.liaoxuefeng.com/wiki/896043488029600)
- [Pro Git](https://git-scm.com/book/zh/)
- [易百教程](https://www.yiibai.com/git)

## Github 的使用

> GitHub是通过Git进行版本控制的软件源代码托管服务平台

- [Github 维基百科](https://zh.wikipedia.org/wiki/GitHub)

- [Github 使用教程图文详解](https://juejin.im/post/5d635670e51d4561e721df15)

- [GitHub 漫游指南](https://github.phodal.com/)

  