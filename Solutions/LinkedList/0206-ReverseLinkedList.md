# 反转链表
## 题目
反转一个单链表。

**示例：**
```
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

**进阶:**
你可以迭代或递归地反转链表。你能否用两种方法解决这道题？

## 解法
### 迭代解法
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
 * @return {ListNode}
 */
let reverseList = function(head) {
    let pre = null, curr = head, tmp;
    while(curr) {
        tmp = curr.next;
        curr.next = pre;
        pre = curr;
        curr = tmp;
    }
    return pre;
};
```
### 递归解法
```js

```
## 思路
没什么好说的，从头到尾逐渐将其前继设置为当前节点的后继即可。

递归暂时还不会~
