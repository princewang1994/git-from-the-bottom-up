# 存储在Tree中的blob

现在我们知道了，Git中所有文件的内容都被存储在一个个Blob中，但是这些blob完全不保存元信息——它们既没有文件名，也没有目录结构，他们仅仅只是“blob”而已。因此，为了让Git能够管理这些文件的结构和名称等元信息，Git的设计者将这些叶子节点绑定在一棵“树”上。由于一个blob可能属于很多棵树，我们无法仅仅通过查看blob知道他是属于哪一棵树的，但我们知道，这个blob一定被包含在我刚刚创建的这个commit的某个地方：

 ```shell
$ git ls-tree HEAD
100644 blob af5626b4a114abcb82d63db7c8082c3c4756e51b greeting
 ```

根据上面执行的命令我们知道，我们在上一节创建的第一个commit包含了一棵树，这棵树只有一个叶子，也就是文件`greating`的内容的blob。虽然我可以把HEAD指针传递给`ls-tree`来查看HEAD指向的commit包含了哪些blob，但我们无法知道这棵树是如何存储的。这里我们有另外一些命令来显示我们系统上的树：

```shell
$ git rev-parse HEAD
588483b99a46342501d99e3f10630cfc1219ea32 # different on your system

$ git cat-file -t HEAD
commit

$ git cat-file commit HEAD
tree 0563f77d884e4f79ce95117e2d686d7d6e282887
author John Wiegley <johnw@newartisans.com> 1209512110 -0400
committer John Wiegley <johnw@newartisans.com> 1209512110 -0400
Added my greeting
```

- 第一条命令把HEAD指向的commit所表示的Hash码打印出来（在这里commit也是被存储在磁盘上，用一个hash来表示）
- 第二条命令用来输出这个指针指向的Hash代表一个什么东西（blob，tree或者是commit），返回结果是commit
- 第三条命令，列出这个commit中包含的内容，显然，这个commit包含了一棵树，不过commit还存储着一些其他的信息，比如作者，comment，提交时间等等。

这里有一点要注意的是，commit的Hash码在我的机器上是独一无二的，如果读者和我一样执行同一条命令，会在控制台输出完全不同的Hash码，这是为什么呢，因为Commit不仅包含了tree的内容，同时也包含了我的名字和我提交的日期，但是第三条命令输出的tree的hash码的输出，读者和我应该是一样的，因为tree中只包含了它所拥有的blob的引用，并且名字也是相同的。

让我们来确认一下，第三条命令中输出的tree是不是就是我们所创建的树：

```shell
$ git ls-tree 0563f77
100644 blob af5626b4a114abcb82d63db7c8082c3c4756e51b greeting
```

现在我们总结一下：在我的仓库中有一个commit（588483b），这个commit包含了一棵树（0563f77），这棵树包含了一个blob（af5626b），而blob保存着文件greeting的内容（Hello world!）。另外我们还有一条命令可以确认一下刚才说的这些事实：

```shell
$ find .git/objects -type f | sort
.git/objects/05/63f77d884e4f79ce95117e2d686d7d6e282887
.git/objects/58/8483b99a46342501d99e3f10630cfc1219ea32
.git/objects/af/5626b4a114abcb82d63db7c8082c3c4756e51b
```

从上面的输出我们可以看出整个仓库中包含了三个对象，而且这三个对象的Hash码都已经出现在了我们前面的例子中。让我们最后执行一条命令，列出这些对象的类型（commit，tree或blob）来满足一下我们我们的好奇心~

```shell
$ git cat-file -t 588483b99a46342501d99e3f10630cfc1219ea32
commit
$ git cat-file -t 0563f77d884e4f79ce95117e2d686d7d6e282887
tree
$ git cat-file -t af5626b4a114abcb82d63db7c8082c3c4756e51b
blob
```

这个时候我们可以使用show命令来简明的列出这些对象包含的内容，具体的操作留给读者作为练习。

