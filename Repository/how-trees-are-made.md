# Tree是如何生成的

有了前几章的知识，我们知道每一个Commit都维护着一棵树（Tree），那么这些树是如何生成的呢，本节我们就来详细讨论这个问题。我们首先要知道，把文件的内容存储在Git仓库中，这就生成了一个Blob，而树“拥有”着一些blob。但我们还不知道这些包含着blob的树是如何被创建的，或者说，这些树是如何链接到他们对应的commit的。

让我们再以一个小例子来开始这一节，我们重新创建一个Git仓库，但这回我们使用底层命令手动构造树，这样可以让读者更清楚的明白这些操作背后发生了什么：

```shell
$ rm -fr greeting .git
$ echo 'Hello, world!' > greeting
$ git init
$ git add greeting
```

当你把一个文件放入index（也就是这里的git add命令）以后，所有的一切就开始了。当我把`greeting`文件加入到index的时候，我的仓库中发生了一些变化。虽然我暂时还不能把这种变化看做是一个Commit，我们可以用下面的方法来看看在我的仓库中究竟发生了什么：

```shell
$ git log # 这条命令将会报错，因为到此为止我们还没有做任何提交
fatal: bad default revision 'HEAD'
$ git ls-files --stage # 把index中引用的所有blob列出来
100644 af5626b4a114abcb82d63db7c8082c3c4756e51b 0 greeting
```

令人疑惑的是，既然我还没有使用git commit命令向我的这个仓库提交任何东西，那么仓库中为什么已经生成了一些blob呢？而且如果读者还有印象的话，这个Hash码与我们之前几章中greeting的Hash码完全一致。因此我知道这个blob其实就代表了我们的greeting文件。这个时候我可以使用`cat-file -t HASHID`命令查看这个blob的类型其实是一个blob，事实上这个blob也就和我们前几章创建的一样的。而正如我们之前一直强调的，相同的文件在Git中总是使用同样的blog和hashid来表示。（原谅我我不厌其烦的强调这个知识点）

不过这个blob现在还不是一棵树，而且我们现在也没有任何Commit，准确的说，此刻这个blob只是存在`.git/index`中，这个目录是用来暂存我们的工作目录的内容，里面的blob组成了我们当前的索引（index），OK，我们现在可以开始生成一棵真正的树了：

```shell
$ git write-tree # record the contents of the index in a tree
0563f77d884e4f79ce95117e2d686d7d6e282887
```

这个Hash码大家应该很熟悉，就是我们上一章也见过同样的Hash（不记得的同学可以翻到上一章去看看），和blob一样，包含了同样的blob的树也会使用同样的Hash编码表示，这也是我们之前提到的。我们还没有创建Commit，但是在Index里面，已经有了一个包含了`greeting`这个blob的tree对象了，因此我们使用`write-tree`这条底层命令来手动创建一棵树，这条命令会把当前Index中的所有内容打包成一棵新的树，以便后续Git使用这棵树来构造一个新的Commit。

我们现在使用`commit-tree`命令，将刚才生成的这一棵树打包成一个真正的Commit：

```shell
$ echo "Initial commit" | git commit-tree 0563f77
5f1bc85745dcccce6121494fdd37658cb4ad441f
```



