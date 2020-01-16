# 删除排序链表中的重复元素
## 题目
给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。

示例一：
```
输入: 1->1->2
输出: 1->2
```

示例二：
```
输入: 1->1->2->3->3
输出: 1->2->3
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
 * @return {ListNode}
 */
var deleteDuplicates = function(head) {
    let initHead = head;
    let nextNode;
    while (head) {
        nextNode = head.next;
        // 由于可能包含多个重复值，因此不断删除直至到尾端或无重复值
        while (nextNode && head.val === nextNode.val) {
            nextNode = nextNode.next
        }
        head.next = nextNode;
        head = head.next;
    }
    return initHead;
};
```
## 思路

解题思路不难，就是将当前 ``ListNode`` 的``next`` 指针打到下一个非重复值上去。问题在于 ``ListNode`` 的 ``next`` 比较绕，注意不要越界和绕晕了。