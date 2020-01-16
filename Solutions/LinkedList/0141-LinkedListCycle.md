# 环形链表
## 题目
给定一个链表，判断链表中是否有环。

为了表示给定链表中的环，我们使用整数 ``pos`` 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 ``pos`` 是 ``-1``，则在该链表中没有环。

**示例 1：**
```
输入：head = [3,2,0,-4], pos = 1
输出：true
解释：链表中有一个环，其尾部连接到第二个节点。
```
![image](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist.png)

**示例 2：**
```
输入：head = [1,2], pos = 0
输出：true
解释：链表中有一个环，其尾部连接到第一个节点。
```
![image](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test2.png)

**示例 3：**
```
输入：head = [1], pos = -1
输出：false
解释：链表中没有环。
```
![image](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test3.png)

**进阶：**
你能用 O(1)（即，常量）内存解决此问题吗？

## 解法
### 解法一：利用``Set``保存每个``ListNode``的指针
```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */

/**
 * @param {ListNode} head
 * @return {boolean}
 */
var hasCycle = function(head) {
    // 使用一个set存储ListNode的指针，在不断next过程中如果发现在set中的指针时，说明有环路
    // 否则会直接走到null，则返回false
    let nodeSet = new Set();
    while (head) {
        nodeSet.add(head);
        head = head.next;
        if (nodeSet.has(head)) {
            return true;
        }
    }
    return false;
};
```
### 解法二：使用快慢指针
```js
```

## 思路
1. 使用暴力法求解的思路比较简单，用``Set``保存每个遍历过的``ListNode``的引用，只要下次碰到已经遍历过的``ListNode``说明必有环路；
2. 后面查看解答发现LeetCode官方解答给了一个**快慢指针**的求解方法。类似于两个速度一块一慢的运动员，快的先跑，如果能追上慢的表明必有环路。