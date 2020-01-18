# 删除链表中的节点
## 题目
请编写一个函数，使其可以删除某个链表中给定的（非末尾）节点，你将只被给定要求被删除的节点。

现有一个链表 ``head = [4,5,1,9]``，它可以表示为:

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/01/19/237_example.png)

**示例 1:**
```
输入: head = [4,5,1,9], node = 5
输出: [4,1,9]
解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
```

**示例 2:**
```
输入: head = [4,5,1,9], node = 1
输出: [4,5,9]
解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.
```

**说明:**
- 链表至少包含两个节点。
- 链表中所有节点的值都是唯一的。
- 给定的节点为非末尾节点并且一定是链表中的一个有效节点。
- 不要从你的函数中返回任何结果。

## 解法
```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} node
 * @return {void} Do not return anything, modify node in-place instead.
 */
let deleteNode = function(node) {
    // 解题思路为将node节点的前继的next设置为node的后继
    // node的后继很好获取，难点在如何获取node的前继
    // 不会做，查看了LeetCode的官方解析：
    // 既然找不到node的前继，那么就把当前节点改成后继
    node.val = node.next.val;
    node.next = node.next.next;
};
```
## 思路

按照常规思路来理解，要删除``node``节点，我们会这么做：将``node``节点的前驱节点的``next``指针指向``node``节点的后继节点``node.next``，也就是跨过``node``节点。但是存在的问题是**我们无法获取到``node``节点的前驱节点**！

后来看LeetCode的官方解答，其非常巧妙的把当前的``node``值设置为``node.next``值，然后跳过``node.next``，脑筋急转弯~
