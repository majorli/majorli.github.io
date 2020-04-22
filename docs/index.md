# Welcome to MajorLi's Blogs

## What's New

**2020年4月22日：**

- C++算法编程指南的2.5.3节“归并排序”校对完成，但是一篇太少了，暂时先放在 draft 里，等校对多几篇在一起发布出去吧。
- 终于搞定了Vim 8在编辑markdown文件时的各种syntax问题。

    Windows gVim 8.2的问题是markdown.vim中 ``*`` 型标记的 ``markdownBold`` 等三个 ``region`` 定义语句中 ``skip="\\*"`` 这个正则pattern写错了，改成 ``skip="\\\*"`` 就好了；

    macOS vim 8.1 的问题不确定是不是因为在 ``_`` 型标记的 ``region`` 定义语句中 ``start`` 和 ``end`` 的pattern中把 ``\w`` 写成了 ``\S``。不过用 ``syntax include`` 把数学公式块定义为第二种语法规则（Tex语法）就好了。顺手改了改 ``.vimrc`` 文件，现在对 VimScript 越来越了解了。

- 试着写了一点算法笔记，约定了伪码的语法规则，写了一段埃氏质数筛算法。决定在这里的 Algorithms 算法笔记里还是不要给源代码了，只给出算法伪码就好，那些太简单的算法也不收录了。BTW，material-mkdocs的视觉效果真的好！

## Projects


### C++算法编程指南

这个项目是给算法编程的初学者编写的学习讲义，使用C++作为编程语言，难度系数大约为NOI竞赛的普及组和提高组。

请查看[项目简介](projects/algo_guide.md)以获取更多信息。

## Algorithms

算法笔记集中收录经典算法和算法问题，为“C++算法编程指南”项目的笔记整理。

此区域目前正在建设中。

## Data Structures

数据结构笔记集中收录各种基础和重要的数据结构，亦为“C++算法编程指南”项目的笔记整理。

此区域尚未开始建设。

