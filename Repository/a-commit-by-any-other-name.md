## Commit的别名

了解了commit是如何构造和组织了以后，你可以抛开一切复杂的操作，只在心中装着Commit的拓扑结构，并忘记所谓的”tag“，”branch“等术语（前文提到，他们也只是某个commit的别名而已），这个时候可以说你已经了解了“Git之禅”。读者记住这件事情应该不是非常困难，在接下来的章节中，希望大家能够把这些放在心里。

如果吧commit比作钥匙，那么你如何命名这些commit则是通往精通的大门。我们有非常，非常多的方式可以给某个，某些commit，甚至是commit包含的blob命名，这些命名方式可以被绝大多数的Git命令所无差别的使用，在这里，我们总结一些常用的commit别名用法：

- `Branchname`：如前面的章节所述，分支是commit的别名，branch和tag的主要区别是tag是无法修改其指向位置的（当然，你也可以删掉重新建立tag），而branch却是可变的，当一个新的提交形成的时候，branch指针将会移动到新建commit上。

- `tagname`: 和branch一样，从commit的角度来说，标签（tag）也是一种别名。其与branch不同的地方在于，标签一旦指向某个commit，则不会修改。

- HEAD: 当前branch指向的节点的最新节点我们把他叫做”HEAD“，如果你检出（checkout）某个commit，而不是检出某个branch的话，这个时候HEAD将会引用这个commit，但这个commit不属于任何一个分支。要特别注意的是，在这种特殊情况下，我们把这样的HEAD叫做”游离的HEAD“。

- **c82a22c39cbc32…**：不管如何，commit总是可以他对应的完整40位hash码来表示的，通常这种方式都是通过”复制-粘贴“得到的，因为我们有其他更方便的方式，因此引用完整hash码的方式不是很常用。

- **c82a22c**：其实只需要使用很少的hash码位数就可以在你的仓库中唯一确定一个commit了，大多数时候，6或8位就足够了。

- name^：我们使用^来表示“某个commit的父节点”，如果该节点有多个父节点，则使用第一个。

- name^^: 我们使用两个连续的^代表“某个commit父节点的父节点”。

- name^2:如果某个节点有多个父节点（一个典型的例子是该节点是两个节点合并后的节点），你可以用name^n表示该节点的第n个父节点。

- **name~10**：在commit后面加一个"~"用来表示改节点的前10代祖先，这种用法常常出现在`rebase -i`中，举个例子，”请列出某个分支最近的commit“。这种用法等价于`name^^^^^^^^^^`。

- name:path：在commit引用后加冒号和路径，用来表示这个commit包含的特定文件，这种引用方法常用于精确显示某个commit下的文件或者使用"git diff"命令比较同一个文件的不同版本:

  ```bash
  $ git diff HEAD^1:Makefile HEAD^2:Makefile
  ```

- **name^{tree}** : 你也可以引用这个分支所包含的树，而不是引用这个commit本身（前文我们有提到，tree和commit的区别）
- **name1..name2**：本条以及之后的别名，均用来表示”commit的范围“，即一组commit，这种引用方式在一些时候特别有用，像一些日志的展示。比如你想要知道一个特定时间段里面我们的版本库发生了什么修改。注意这种语法中，我们只引用了name2向前至name1的commit，但不包含name1，如果省略了name1或者name2，Git会使用HEAD作为默认值。
- name1…name2：与上面的区别是，有三个点。对于log之类的命令，它引用name1或name2引用的所有commit，但如果二者有重复，则不会重复引用。结果是两个分支中所有唯一commit的列表。
- **master..**：折哟在那个用法等价于"master..HEAD"，其实和name1..name2，没有区别，之所以把这种引用方式放在这里，是因为我经常使用这种方法来review从master到目前分支所做的改动。
- ..master: 和上面的方式一样，这种方式在一些时候特别有用，比如你刚刚从远程fetch下来一些commit，然后想看看从上一次rebase或者merge以后你修改了那些文件。
- **–since=“2 weeks ago”**：引用特定日期之后的commit
- **–until=”1 week ago”**：引用特定日期之前的commit
- **–grep=pattern** ：引用message中包含特定关键字的commit（支持正则表达式）
- **–committer=pattern**：引用那些提交者包含特定关键字的commit
- **–author=pattern**：引用作者包含特定关键字的commit，这里解释一下”提交者“和“作者”的关系：作者是创建这个commit的人。在本地工作的时候，开发者通常来说既是提交者，又是作者，然而某些不定可以通过e-mail发送，然后在另外一个版本库提交，这个时候”写这份代码的人“和”提交这份代码的人“可能就不是同一个了，因此区别开来。
- **–no-merges**：引用所有只有一个父节点的commit，忽略那些合并节点。

以上的这些用法大多数可以混合使用，我们也给出一个例子，来寻找从master分支到目前分支的commit中，我自己近一个月内提交的包含message”foo“的commit：

```bash
$ git log --grep='foo' --author='johnw' --since="1 month ago" master..
```

