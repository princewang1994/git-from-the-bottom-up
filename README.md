# 自底向上理解Git（Git: From the Bottom UP）

原文地址：[https://jwiegley.github.io/git-from-the-bottom-up/](https://jwiegley.github.io/git-from-the-bottom-up/)

本书GitBook地址：[https://legacy.gitbook.com/book/princewang1994/git-from-the-bottom-up/details](https://legacy.gitbook.com/book/princewang1994/git-from-the-bottom-up/details)

\[TOC\]

## Motivation

Git是目前最流行的版本控制工具，从Git工具出发衍生出的软件开发，集成环境不计其数，然而对许多新入门的同学而言，Git繁多的选项，复杂的命令，都给入门带来了一些困难。互联网上不乏Git的快速入门教程（如廖雪峰老师的博客），对于入门新手而言，在阅读完这些教程以后，完全可以完成一些Git的日常操作如Add，Commit，Push等操作，然而当更加复杂的命令，如Git的分支操作，暂存等等高级操作时，那些比较难懂的命令（如Reset和Rebase）就会带来不小的困难。在这个时候，从底层了解一些Git的设计思想和原理，能够帮助新人们快速了解Git的设计哲学，对于老手来说，也可以温故知新。本文是一篇非常好的Git原理性文章，通俗易懂，而且带有一些小例子，也是本人从入门Git以后提升的重要资料，在工作之余翻译，也纯属娱乐，希望能够帮助到一些刚入门的同学。本人英文水平有限，在措辞和整体翻译上可能还有一些偏差，希望各位看官们见谅。

在此声明：本文的翻译出于个人学习，不包含任何商业目的，如有侵犯作者权益，立即删除

## Content

## 1. Repository

* [Introduction](/README.md)
* [Repository: 目录内容最终追踪](/Repository/repository-directory-content-tracking.md)
* Blob简介
* 存储在Tree中的blob
* Tree是如何生成的
* 优美的提交（Commit）
* Commit的其他表示方法
* 分支与Rebase的力量
* 迭代式Rebase

## 2. 索引（The Index）

* 作为中间人的Index
* 更深入理解Index

## 3. 重置（Reset）

* 重置与否？是个问题
* 混合重置
* 软重置（Soft Reset）
* 硬重置（Hard Reset）

## 4. 暂存（Stashing）与 引用日志（reflog）

* 暂存（Stashing）与 引用日志（reflog）

## 5. 总结

* 总结

## 6. 延伸阅读

衍生阅读

## 联系我

如有任何对本书的意见或建议，欢迎联系我！

**E-mail**: princewang1994@gmail.com

**个人主页:**

http://blog.prince2015.club

http://princewang1994.github.io







