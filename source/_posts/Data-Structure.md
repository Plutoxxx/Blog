---
title: 数据结构与算法
top: false
cover: false
toc: true
mathjax: true
date: 2020-06-10 20:18:31
password:
summary: 总结一下数据结构、算法相关的知识。
tags:
    - 数据结构与算法
categories:
    - Java
---
<div align="middle"><iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=26116370&auto=1&height=66"></iframe></div>

# 常见的数据结构
---
数据存储的常用结构有：栈、队列、数组、链表和二叉树。我们分别来了解一下：

## 栈

* **栈**：**stack**,又称堆栈，它是运算受限的线性表，其限制是仅允许在标的一端进行插入和删除操作，不允许在其他任何位置进行添加、查找、删除等操作。

简单的说：采用该结构的集合，对元素的存取有如下的特点

* 先进后出（即，存进去的元素，要在后它后面的元素依次取出后，才能取出该元素）。例如，子弹压进弹夹，先压进去的子弹在下面，后压进去的子弹在上面，当开枪时，先弹出上面的子弹，然后才能弹出下面的子弹。

* 栈的入口、出口的都是栈的顶端位置。
![](堆栈.png)

这里两个名词需要注意：

* **压栈**：就是存元素。即，把元素存储到栈的顶端位置，栈中已有元素依次向栈底方向移动一个位置。
* **弹栈**：就是取元素。即，把栈的顶端位置元素取出，栈中已有元素依次向栈顶方向移动一个位置。

* 常用方法：
 - `public boolean empty()`：测试此堆栈是否为空。
 - `public E peek()`：查看此堆栈顶部的对象，而不从堆栈中删除它。
 - `public E pop()`：删除此堆栈顶部的对象，并将该对象作为此函数的值返回。
 - `public E push(E item)`：将项目推送到此堆栈的顶部。
 - `public int search(Object o) `：返回一个对象在此堆栈上的基于1的位置。

### 相关题目

1. 栈的压入、弹出序列
输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）

```java
import java.util.ArrayList;
import java.util.Stack;
public class Solution {
    public boolean IsPopOrder(int [] pushA,int [] popA) {
        Stack<Integer> temp = new Stack<>();
        int i=0;
        for(int num: pushA){
            temp.push(num);//入栈
            //模拟出栈
            while(!temp.isEmpty() && temp.peek()==popA[i]){
                i++;
                temp.pop();
            }
        }
        return temp.isEmpty();
    }
}
```

## 队列

* **队列**：**queue**,简称队，它同堆栈一样，也是一种运算受限的线性表，其限制是仅允许在表的一端进行插入，而在表的另一端进行删除。

简单的说，采用该结构的集合，对元素的存取有如下的特点：

* 先进先出（即，存进去的元素，要在后它前面的元素依次取出后，才能取出该元素）。例如，小火车过山洞，车头先进去，车尾后进去；车头先出来，车尾后出来。
* 队列的入口、出口各占一侧。例如，下图中的左侧为入口，右侧为出口。

![](队列图.bmp)

* 常用方法：
 - `public boolean add(E e)`：将指定的元素插入到此队列中。
 - `public E peek()`：检索但不删除此队列的头，如果此队列为空，则返回 null 。 
 - `public E pop()`：检索并删除此队列的头，如果此队列为空，则返回 null 。 
 - `public E remove() `：检索并删除此队列的头。 

## 数组

* **数组**:**Array**,是有序的元素序列，数组是在内存中开辟一段连续的空间，并在此空间存放元素。就像是一排出租屋，有100个房间，从001到100每个房间都有固定编号，通过编号就可以快速找到租房子的人。

简单的说,采用该结构的集合，对元素的存取有如下的特点：

*  查找元素快：通过索引，可以快速访问指定位置的元素

  ![](数组查询快.png)

*  增删元素慢
  * **指定索引位置增加元素**：需要创建一个新数组，将指定新元素存储在指定索引位置，再把原数组元素根据索引，复制到新数组对应索引的位置。如下图：![](数组添加.png)
  * **指定索引位置删除元素：**需要创建一个新数组，把原数组元素根据索引，复制到新数组对应索引的位置，原数组中指定索引位置元素不复制到新数组中。如下图：![](数组删除.png)

## 链表

* **链表**:**linked list**,由一系列结点node（链表中每一个元素称为结点）组成，结点可以在运行时i动态生成。每个结点包括两个部分：一个是存储数据元素的数据域，另一个是存储下一个结点地址的指针域。我们常说的链表结构有单向链表与双向链表，那么这里给大家介绍的是**单向链表**。

  ![](单链表结构特点.png)

简单的说，采用该结构的集合，对元素的存取有如下的特点：

* 多个结点之间，通过地址进行连接。例如，多个人手拉手，每个人使用自己的右手拉住下个人的左手，依次类推，这样多个人就连在一起了。

  ![](单链表结构.png)

* 查找元素慢：想查找某个元素，需要通过连接的节点，依次向后查找指定元素

* 增删元素快：

  *  增加元素：只需要修改连接下个元素的地址即可。

    ![](增加结点.png)

  *  删除元素：只需要修改连接下个元素的地址即可。

    ![](删除结点.bmp)

* 常用方法：
 - `public boolean add(E e)`：将指定的元素追加到此列表的末尾。 
 - `public void add(int index, E element) `：将指定的元素追加到此列表的末尾。 
 - `public boolean contains(Object o)`：如果此列表包含指定的元素，则返回 true 。
 - `public E get(int index)`：返回此列表中指定位置的元素。 
 - `public E peek()`：检索但不删除此列表的头（第一个元素）。
 - `public E poll()`：检索并删除此列表的头（第一个元素）。
 - `public E push(E e)`：将元素推送到由此列表表示的堆栈上。
 - `public E pop()`：从此列表表示的堆栈中弹出一个元素。
 - `public E remove() `：检索并删除此列表的头（第一个元素）。
 - `public E removeLast() `：从此列表中删除并返回最后一个元素。
 - `public int size() `：返回此列表中的元素数。 

### 相关题目

1. 反转链表
输入一个链表，反转链表后，输出新链表的表头。
```java
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
public class Solution {
    public ListNode ReverseList(ListNode head) {
        if(head == null){
            return null;
        }
        ListNode pre = null;
        ListNode cur = head;
        while (cur != null){
            ListNode next = cur.next;
            cur.next = pre;
            //将链表的两个节点右移
            pre = cur;
            cur = next;
        }
        return pre;
    }
}
```

## 二叉树

* **二叉树**：**binary tree** ,是每个结点不超过2的有序**树（tree）** 。

简单的理解，就是一种类似于我们生活中树的结构，只不过每个结点上都最多只能有两个子结点。

二叉树是每个节点最多有两个子树的树结构。顶上的叫根结点，两边被称作“左子树”和“右子树”。

如图：

![](二叉树.bmp)

### 相关题目

1. 重建二叉树
输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。

```java
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    private static int index = 0;
    private static TreeNode solve(int[] pre, int[] tempIn) {
        int len1 = 0; /// 当前节点的左子树的节点的个数
        int len2 = 0; /// 当前节点的右子树的节点的个数
        for (int i = 0; i < tempIn.length; i++) {
            if (pre[index] == tempIn[i]) {
                break;
            }
            len1 ++; /// 左子树节点的个数++
        }
        len2 = tempIn.length - len1 - 1;

        int index1 = 0;
        int index2 = 0;
        int[] temp1 = new int[len1]; /// 当前节点的左子树
        int[] temp2 = new int[len2]; /// 当前节点的右子树
        boolean flag = false; //设置判断标志false->当前中序的值为左子树中的值，true->当前中序的值为右子树中的值
        for (int i = 0; i < tempIn.length; i++) {
            if (pre[index] == tempIn[i]) {
                flag = true;
            } else if (!flag) {
                temp1[index1++] = tempIn[i];//存放左子树的值
            } else {
                temp2[index2++] = tempIn[i];//存放右子树的值
            }
        }
        TreeNode node = new TreeNode(pre[index]);//node为重建树后的节点
        node.right = null;
        node.left = null;
        if (index < pre.length && temp1.length > 0) {
            index++; /// 遍历前序序列的下标加1
            node.left = solve(pre, temp1); /// 创建当前节点的左子树
        }
        if (index < pre.length && temp2.length > 0) {
            index++; /// 遍历前序序列的下标加1
            node.right = solve(pre, temp2); /// 创建当前节点的右子树
        }
        return node;
    }
    public TreeNode reConstructBinaryTree(int [] pre,int [] in) {
        index = 0;
        return solve(pre, in);
    }
}
```

2. 打印二叉树
从上往下打印出二叉树的每个节点，同层节点从左至右打印。

```java
import java.util.ArrayList;
import java.util.Queue;
import java.util.LinkedList;
/**
public class TreeNode {
    int val = 0;
    TreeNode left = null;
    TreeNode right = null;

    public TreeNode(int val) {
        this.val = val;

    }

}
*/
public class Solution {
    public ArrayList<Integer> PrintFromTopToBottom(TreeNode root) {
        ArrayList<Integer> ans = new ArrayList<>();
        Queue<TreeNode> queue = new LinkedList<>();//存放二叉树节点
        if(root != null){
            queue.add(root);
        }
        while(!queue.isEmpty()){
            //取出队列中的节点
            TreeNode node = queue.poll();
            //保存树中的节点到ArrayList
            ans.add(node.val);
            //同层节点从左到右打印
            if(node.left != null) queue.add(node.left);
            if(node.right != null) queue.add(node.right);
        }
        return ans;
    }
}
```