# 移除链表元素
## 题目
删除链表中等于给定值 ``val`` 的所有节点。

**示例：**
```
输入: 1->2->6->3->4->5->6, val = 6
输出: 1->2->3->4->5
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
 * @param {number} val
 * @return {ListNode}
 */
var removeElements = function(head, val) {
    // 针对空链表直接返回
    if (!head) {
        return head;
    }
    // 第一个元素
    let initHead;
    if (head.val === val) {
        while (head && head.val === val) {
            head = head.next;
        }
        initHead = head;
    } else {
        initHead = head;
    }
    // 之后不断移除相同元素
    while(head && head.next) {
        while (head.next && head.next.val === val) {
            head.next = head.next.next
        }
        head = head.next
    }
    return initHead;
};
```
## 思路
题目思路很简单，但是答案写得丑的要死，分享下LeetCode的官方答案：
```python
class Solution:
    def removeElements(self, head: ListNode, val: int) -> ListNode:
        # 首先设置了哨兵
        sentinel = ListNode(0)
        sentinel.next = head
        
        # 前驱和当前节点
        prev, curr = sentinel, head
        while curr:
            # 如果当前节点的值重复时，前驱的后继不断往后跳
            if curr.val == val:
                prev.next = curr.next
            else:
                prev = curr
            curr = curr.next
        
        return sentinel.next
```
