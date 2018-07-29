# 引言

欢迎来到Git的世界，写这篇文档的初衷是能够帮助读者对Git这个强大的版本控制工具更深入的理解。Git从外部来看是比较复杂的，比如它拥有太多令人眼花缭乱的选项，但是通过这篇文档，我将解释Git的原理其实是非常简洁的。

在我们深入了解之前，便于读者理解，我们需要先列出一些名词，这些名次将会在后面的章节中被反复使用到：

* **仓库（Repository）**：一个仓库是提交（Commit）的集合，每个Commit都是当前的_工作目录树_在一个过去特定时间点的存档，不管是在你自己的，还是在其他人的机器上。在仓库中也会定义一个HEAD指针（后面会讲到），这个HEAD指针是用来指向当前工作目录树所在的Commit或Branch。最后，仓库中还包括了一些其他变量，如分支（ branches）和标签（tags），用来指向某一个commit，也可以理解为是一个Commit的别名
* **索引（Index）**：不同于许多其他版本控制的工具，Git不会把一个提交里面的所有改变从工作目录树直接提交到版本仓库。而是先生成一个叫做索引（Index）的东西。想象一下，索引就是一个可以“确认”你的提交的地方，在你提交版本变化之前，把你修改了的文件一个一个的放进索引中。一些人喜欢用一个更加直观的词“暂存区”，而不是“索引”来称呼他。
* **工作目录树（Working Tree）**：工作目录树是任何一个文件系统上，并存有仓库配置信息的目录。（存有配置信息通常是指在该目录中存在.git子目录）工作目录树包含了你需要版本管理的所有的文件与子目录。
* **提交（Commit）**：一个提交就是工作目录树在某一个时间点的快照。在你提交某一个新的变化的时候，HEAD指针当前指向的Commit就会变成新的Commit的父节点。这就产生了“修订历史”这个概念。
* **分支（Branch）**：分支其实只是一个Commit的别名而已（更加具体的我们将会在以后的具体讲到Commit的时候说道），我们也称分支为“引用”。就是这种提交与提交之间的父子关系组成了提交的整个历史，因此也产生了所谓“开发分支”的说法。
* **标签（Tags）**：标签和分支一样，也是Commit的一个别名，区别在于，标签总是指向某一个Commit，基本不会改变，并且标签有着自己的描述文字。

* **主分支（Master）**：在一个项目（仓库）中，通常我们把开发的主线分支叫做**master**分支。注意这里只是典型约定俗成，并没有规定主分支的名字一定是master

* **HEAD指针**：HEAD指针是用来指向一个提交（Commit）或分支（Branch）：

  * 如果你检出一个分支，那么HEAD指针就将会指向这个分支（译者注：初始化时HEAD指向master分支所对应的Commit），而当你创建一个提交的时候，HEAD指针将会指向这个新的提交，而这个HEAD指针原来指向的提交将会变成这个提交的父节点。

  * 如果你检出一个Commit，那么HEAD指针只会指向这个Commit，不会随着新的提交而移动，此时我们称这个HEAD指针叫做“游离的HEAD”，举个例子，这种情况发生在你检出了一个标签的时候。

通常的一个典型的工作流是这样的：首先创建一个仓库，接着你对这个仓库所在的工作目录进行修改（比如添加文件或修改文件内容）一旦你的工作到达了一个比较有意义的节点，比如修复了一个bug，一天工作的结束，或某一时刻所有代码全部辨已完成，你就可以把你修改好的文件一个一个加入索引中。当你需要提交的所有文件都已经包括在索引中了，你就可以创建一个提交来记录当前工作目录树中的所有内容。下图是一个典型的项目生命周期：

![](/assets/overview.png)

读者可以先将这张图记在心中，在接下来的章节中，我们会详细讲述这张图中的每一个部分是对于Git版本管理操作的重要作用。

