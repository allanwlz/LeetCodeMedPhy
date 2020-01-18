# 二进制链表转整数
## 题目
给你一个单链表的引用结点 ``head``。链表中每个结点的值不是 0 就是 1。已知此链表是一个整数数字的二进制表示形式。

请你返回该链表所表示数字的**十进制值**。

**示例 1：**

![image](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/12/15/graph-1.png)
```
输入：head = [1,0,1]
输出：5
解释：二进制数 (101) 转化为十进制数 (5)
```

**示例 2：**
```
输入：head = [0]
输出：0
```

**示例 3：**
```
输入：head = [1]
输出：1
```

**示例 4：**
```
输入：head = [1,0,0,1,0,0,1,1,1,0,0,0,0,0,0]
输出：18880
```

**示例 5：**
```
输入：head = [0,0]
输出：0
```

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
 * @param {ListNode} head
 * @return {number}
 */
let getDecimalValue = function(head) {
    // 二进制数左移，相当于乘以2。链表指针
    let sum = 0;
    while (head) {
        sum = sum * 2 + head.val;
        head = head.next;
    }
    return sum;
};
```
## 思路

这道题最傻的解法是使用一个

然而实际更好的解法是将链表指针右移的过程理解为整个链表（二进制数）在左移的过程。
