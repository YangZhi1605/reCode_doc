>**现在清楚了基本的使用语法，规则，那么，直接上项目了。大骨架立起来，现在填充血肉**

# Start

主要是去github拉前后台自己需要的项目了。此处也需要利用复利效应滚动起来。

**关于github的项目**

一、看README文档和相关文档，干嘛了？了解这个项目的功能

二、一定得运行项目。按照我的经验。我想运行起来项目，又可以~~学~~补好多东西了。

三、开始变化了

————>尝试删除一些代码，保证项目能够一直运行

————>把删除的代码一点一点加回来，加的过程，就得自己写笔记干嘛呢？记录这个学习的过程

四、自我学习

————> 有问题就及时检索去解决，

五、反复迭代

————>我理解的这里有两层意思，其一是对项目的迭代，其二是对自己能力的迭代向前。



# Body

### 一、关于一些基本操作

① 在github上创建仓库你是会的。

② 在需要git托管的文件夹中`git init`

③ 目前我的电脑初始化出来是`master`分支，故而需要将分支的名字修改为github上的`main`分支：`git branch -m master main` 进行修改+`git branch`查看分支名称

④ 添加远程仓库`git remote add xxxSSH`来添加，以及通过`git remote -v`来查看远程仓库的名称

⑤ `add`和`commit`操作了

⑥ 推送到远程仓库：``git push -u origin main` `

⑦ 加入需要拉取再推送，是这种拉取：`git pull origin main `









# Thinking & Question

> 我在本地使用指令`git init`初始化了一个git仓库，我查看它的分支名称是`master`，我想推送到github的仓库的分支是`main`，此我应该如何操作了 ?

==

- 在你的本地仓库中，你可以使用`git branch -m master main`把你的`master`分支名称更改为`main`。`-m`代表移动（也可以理解为重命名），它会创建一个新的名为`main`的分支，并把当前的`master`分支删除。
- 完成上述操作后，你可以使用`git push -u origin main`将你的本地仓库推送到github。`-u`代表设置上游，后面跟着你的远程仓库名（在这里是`origin`）和你的分支名（在这里是`main`）。当你未来在此分支执行`git push`或`git pull`时，Git会知道是向哪个分支推送或者从哪个分支获取更新。

 

​	只需要完成上述两步操作后，你的本地`master`分支就会成功地改名为`main`并且能够正确地推送到github的对应分支上了。

==



>这个指令`git push -u origin main`的`origin`需要更换为我远程仓库的地址，即，于我而言，更为为`git@github.com:YangZhi1605/Graduation_Design_Project.git`。对吗？ 

==

实际上，`origin`在这个上下文中代表的是你的远程仓库别名，而不是你的远程仓库地址。

当你用`git clone`或`git remote add`命令添加远程仓库时，会同时创建一个别名来指向这个远程仓库的URL。默认情况下，这个别名叫做`origin`。

 让我们以`git remote add`为例。当你运行`git remote add origin git@github.com:YangZhi1605/Graduation_Design_Project.git`，你就在本地仓库中创建了一个指向这个远程仓库URL的别名`origin`。完成这个步骤后，你就可以用`origin`来代替`git@github.com:YangZhi1605/Graduation_Design_Project.git`，以后进行`git push`，`git fetch`，`git pull`等操作时都可以使用这个方便的别名。



所以，你无需将`git push -u origin main`中的`origin`替换为你的远程仓库地址，你只需要确保你已经正确地设置了`origin`这个别名就可以了。

==



>在git中，我应该如何查看远程仓库的名称 ?

==

如果你想要查看远程仓库的名称，你可以在 Git Bash 或者任何其他的 Git 终端中使用以下命令：

```
git remote -v
```

这个命令会显示你的远程仓库的所有别名（通常为 `origin`），以及它们对应的 URL。输出可能类似如下：

```
origin  https://github.com/username/repository.git (fetch)
origin  https://github.com/username/repository.git (push)
```

在这里，“origin”就是远程仓库的名称，而 URL 则是这个远程仓库在网络上的地址。

==



>（push）和（fetch）之间有什么区别吗 

==

是的，这两者之间在Git中做的工作是不同的：

1. Fetch：这是一种**下载远程仓库最新更改的操作**，但不会自动合并到你本地的分支。即取得了远程仓库的更新，但不直接影响你的本地工作。如果你想合并这些更改，你需要手动执行 `git merge` 命令。
2. Push：这是一种**将你的本地仓库的修改推送给远程主机的操作**。这实际上是上传了你的更改，使远程仓库与你的本地仓库同步。

 

所以，当你查看远程仓库（`git remote -v`）的时候，通常你会看到两行输出：

分别是用于fetch（拉取）和push（推送）操作的URL。

大多数情况下，这两个URL是一样的，除非你想从一个位置获取更改（fetch），而将更改推送到另一个位置（push）。这通常用于特定的工作流程设置。

==









# Reference



