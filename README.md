当踏入社会，或者需要跳槽的时候，都需要进行面试，一次好的面试发挥，往往会给你后续带来更多福利，无论是`待遇涨幅`，还是`职级 title`。在经过一些成功和失败的面试后，也总结出一些经验，这里将这些经验无私地分享给各位，希望对你们能有所帮助。如果侥幸帮到了您，别忘了和我分享你的喜悦。

后面文章中提及的代码，在这个 [https://github.com/woaitqs/common_algorithm](https://github.com/woaitqs/common_algorithm) 链接中都有反馈，有兴趣的同学可以fork，我也会时不时更新。

-------------------

### 面试官看重什么

对于有一定规模的公司而言，往往都有成套的面试系统，能够从多方面考察面试者，但大多无出其右，都是四方面的能力。

1. 基础的计算机知识(算法、数据结构、操作系统、网络协议等等);

2. 所从事领域的领域知识(Android开发相关的、后端知识体系、运维相关知识等等);这里以 Android 为例来进行说明，基础的领域知识包括但不限于 `Activity生命周期`(从A启动B，A和B分别经历了什么)、`Handler 机制`、`AsyncTask 的基础实现`、`Android 异常处理机制`。

3. 架构能力(这部分往往针对一些高阶职位，通常问题是让你现场设计并解决一个业务问题);

4. 综合能力(对新技术、新潮流是否关注，是否有基本的沟通能力技巧，高阶职位更会考察对整个团队的把控能力)。

当我们准备面试的时候，我们需要根据自己的职业需求来看。如果是初级岗位，一定要有良好的基础计算机知识，高阶一点的岗位，适当针对自己的简历来表达下自己对产品的`把控能力`，对项目的`推进能力`，表现出自身对团队的`贡献`。

-------------------

### 常用算法面试技巧

接下来，从我自身出发说说如何准备面试。现在我寻求的岗位是高级工程师，介于初级与技术总监的之间，相当于一个项目中的技术骨干，对于这个职位而言，主要是对算法能力与领域能力的要求会多一些。对于领域方面的知识，相信大家在日常的开发中以及有足够的积累了，对于 Android 方面的知识，也可以通过我的博客 [www.woaitqs.cc](http://www.woaitqs.cc) 进行一些补充。重点是算法能力，客户端工程师在平常的开发中，实际需要用到的算法并不是很多，最好在面试之间，再进行一些针对性的学习与联系。

通过简单的面试题，往往就能看出你是否具有对应的素养要求。考察点包括但不限于以及几个方面。

1. 命名规范。如果你笔试的题目里面都是 a1, b3 诸如此类的变量名，大概率面试官会觉得你的代码可读性很差，印象分不会很高。

2. 代码逻辑。面试官希望能从你写的代码里面，看出你的逻辑。如果你的代码里面，有很多层的嵌套，让人一眼看不透你的思路，这样就不是很好的情况。好的代码，能够一遍读下去就很清楚作者的思路。

3. 边界处理。程序的边界处理，一定程度上反映了你的经验，异常清楚处理得好，也能说明你往往很心细，特别是对于服务端，客户端工程师而言，面对的往往是异常复杂的情况，这方面的能力尤为重要。

我们只要保证这三方面表现得好，那么给面试官的印象就不会很差。接下来继续讲解常见的算法技巧，算是最干货的部分啦，：）。

![algorithm](http://o8p68x17d.bkt.clouddn.com/google-code-seo-algorithm9-ss-1920-800x450.jpg)

-------------------

### 窗口的活灵活用

这类题目常见于字符串和数组应用中，通常用于帮助我们优化时间复杂度。通常我们在解决问题的时候，需要多次嵌套循环遍历数组或者字符串，但如果我们引入窗口这个概念，在每次迭代的时候，通过某种规则不断地改变这个窗口，利用这个窗口输出的信息，能够轻松地为下一步决策提供支持，而不用嵌套循环。说得有些抽象，我们从实际的例子出发，看看窗口是怎么帮助我们的。

[最长不重复子串](https://leetcode.com/problems/longest-substring-without-repeating-characters)，给定一个字符串，设计一种算法来找到最长不重复子串的长度。最简单的算法是，嵌套遍历，遍历可能的字符串找到其中最长的。这是一种算法，但时间复杂度过高。这里我们来设定这样一种窗口`S[i,j]`，这个窗口表明在 i 到 j 中出现的字符。这个窗口可以用 Map 来进行表示，当判断 j + 1 这个位置时，只需要判断`S[i,j]`中是否出现了 char[j+1], 这样在窗口的帮助下，就省去了嵌套的步骤。另一方面，还可以对这个窗口进行进一步优化，例如 Map 的存储 `<char, pos>`, 每个字符出现的最新一次位置，当出现重复时，直接将窗口中的 i 更新为 Map 中存放的pos即可。[https://leetcode.com/articles/longest-substring-without-repeating-characters/](https://leetcode.com/articles/longest-substring-without-repeating-characters/)

-------------------

### 空间换时间

这是一种特别的常用的技巧，面试官也很喜欢从这方面来进行考察。例如曾有面试官问我，给出一个100万学生的高考成绩，让我设计一种算法，能够高效地查到 Top 100的成绩。第一印象大家可能抛出 [find the k largest elements in an array](https://leetcode.com/problems/kth-largest-element-in-an-array) 这类的解决方案。但更好的思路是这样的，假定这100万学生的高考成绩在 0 -750 分这个范围内，那么遍历一遍，建立起每个分数与该分数的学生数目之间的关系。在此之后，从750分递减地进行查找，直到数目达到100。这种方式就是常见用空间交换时间的策略。

还有经典题目，[第一次只出现一次的字符](http://zhedahht.blog.163.com/blog/static/25411174200722191722430/)，都是对这一技巧的诠释。

-------------------

### 动态规划

> 动态规划的精髓在于「规划」，在于对问题的规划上面。当我们遇到一系列问题的时候，常常喜欢把复杂的问题分拆成小问题，动态规划也是对复杂问题的拆分，不过动态规划是更高级的拆分形式而已。高级的地方在于，复杂问题拆分成小问题的方式，同样适用于小问题分拆成更小的问题，也适用于更小的问题分拆成更更小的问题，直到不再是问题。

关于动态规划，在我的两篇博文中专门举例说明了，有兴趣的同学可以去看看。[也来谈谈动态规划](http://www.woaitqs.cc/program/2016/04/22/dynamic-programming)
 与 [也来谈谈动态规划-2](http://www.woaitqs.cc/program/2016/09/27/dynamic-programming-2)。

-------------------

### 二叉树

二叉树也是面试官重点考察的方面，但一般不会涉及二叉树特别复杂的操作，面试的点主要是如下三方面。

- 二叉树的前、中、后序

前序是指先遍历根节点，然后是左子树，右子树；中序先遍历左子树，然后是根节点，右子树；后序遍历是左子树，又子树，最后是根节点。这些算法都可以通过递归来实现，这里简单地列出前序遍历的代码。

```java
public static void preTraversal(Node root) {

  if (root == null) {
    return;
  }

  visit(root);
  preTraversal(root.left);
  preTraversal(root.right);

}
```

- 二叉树的层次遍历

除了前面提到的三种遍历方式以外，面试官也还经常考察层次遍历。层次遍历主要用队列来辅助记录遍历信息。

```java
public static void orderTraversal(Node root) {
  LinkedList queueRoots = new LinkedList();
  queueRoots.offer(root);

  while (!queueRoots.isEmpty()) {
      Node current = queueRoots.poll();
      visit(current);
      if (current.left != null) {
        queueRoots.offer(current);
      }
      if (current.right != null) {
        queueRoots.offer(current.right);
      }
      System.out.println("\n");
  }

}
```

- DFS 与 BFS

这两种遍历方式也是需要熟悉的，要知道这两种方式可以分别用 Stack 与 Queue 来实现。篇幅缘故就不在这里展开了。除此以外，一些面试题也往往从这两者中进行展开，例如`最大路径和`等等。

-------------------

### 排序算法

这类面试题几乎是家常便饭，特别是快速排序。最好在面试前手写一下快速排序和归并排序的算法。

- 快速排序

```java
public static void quickSort(int[] array, int start, int end) {
    if (start >= end) {
      return;
    }
    // partition this array to two parts.
    int partProv = partition(array, start, end);
    quickSort(array, start, partProv - 1);
    quickSort(array, partProv + 1, end);
  }

private static int partition(int[] array, int start, int end) {
    int resultIndex = start - 1;
    int compareKey = array[end];
    for (int i = start; i < end - 1; i++) {
      if (array[i] <= compareKey) {
        resultIndex++;
        exchange(array, resultIndex, i);
      }
    }
    exchange(array, resultIndex + 1, end);
    return resultIndex + 1;
  }

private static void exchange(int[] array, int left, int right) {
    int temp = array[left];
    array[left] = array[right];
    array[right] = temp;
  }
```

- 排序算法的基本信息

除了前面的基本算法以外，也需要对这些算法的基础信息了然于心。比如它们的时间复杂度，它们的思想原理等等。

-------------------

### 链表操作

链表是面试官考察的基础方面之一，这里面特别灵活，难度由浅至深，也很容易出一些能够考量面试者能力的题目。

这里罗列一些常见题目，大家可以由此扩散开来。

- 单链表反转

这个题目通常由两种算法来解决，一则是通过头插法（将每一个节点都插入到头部）的方式，或者通过递归的方式来进行。下面代码里面就展示了如何通过递归的方式来实现链表的反转。

```java
public Node reverseList(Node node) {
  if (node == null || node.next == null) {
    return node;
  }
  Node nextNode = node.next;
  nextNode.next = node;
  node.next = null;
  return reverseList(nextNode);
}
```

上面代码的思路，是将一个列表页面分为第一个节点和剩余部分，当把剩余部分看成一个整体时，整个题目就可以认为是反转第一个节点与剩余部分了，再这么继续递归下去，知道只存在一个节点时。

- 倒数第K个数

链表还有一种常见的技巧 -- 多指针。在解决某些问题的时候，单次遍历达不到效果，多次遍历又效率不够，那么多指针就是一种优化的途径。回到小标题的题目上面去，倒数第K个数字，可以这么来解决。第一个指针先走 K 步，然后两个指针同时前移，直到先走的指针到达末尾，此时后走的指针位置即是倒数第 K 个位置。这个思路也可以应用到检查单链表是否成环这样的问题上来。

-------------------

### 常见 Android 领域知识

[Activity正常和异常情况下的生命周期](http://blog.csdn.net/geekerhw/article/details/48749935)

[Service 和 IntentService 的区别](http://blog.qiji.tech/archives/2693)

-------------------

### 总结

在前面的算法章节中，简单地说明了面试官常常考虑的方面，希望对打算找工作的朋友有所帮助。相关代码在这，[https://github.com/woaitqs/common_algorithm](https://github.com/woaitqs/common_algorithm) 欢迎 fork。

------------------------

### 文档信息

* 版权声明：自由转载-非商用-非衍生-保持署名（[创意共享3.0许可证](http://creativecommons.org/licenses/by-nc-nd/3.0/deed.zh)）
* 社交媒体：[weibo.com/woaitqs](http://weibo.com/woaitqs)
* Feed订阅：[www.woaitqs.cc/feed.xml](http://www.woaitqs.cc/feed.xml)

------------------------