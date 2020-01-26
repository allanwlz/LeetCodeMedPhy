# 环形链表II
## 题目
给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 ``null``。

为了表示给定链表中的环，我们使用整数 ``pos`` 来表示链表尾连接到链表中的位置（索引从 ``0`` 开始）。 如果 ``pos`` 是 ``-1``，则在该链表中没有环。

**说明：**不允许修改给定的链表。

**示例 1：**
```
输入：head = [3,2,0,-4], pos = 1
输出：tail connects to node index 1
解释：链表中有一个环，其尾部连接到第二个节点。
```
![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist.png)

**示例 2：**
```
输入：head = [1,2], pos = 0
输出：tail connects to node index 0
解释：链表中有一个环，其尾部连接到第一个节点。
```
![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test2.png)

**示例 3：**
```
输入：head = [1], pos = -1
输出：no cycle
解释：链表中没有环。
```
![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test3.png)

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
let detectCycle = function(head) {
    // 处理无结点及单个非环结点情况
    if (head === null || head.next == null) {
        return null;
    }
    // 快慢指针，快指针在前，慢指针在后，并保存初始结点
    let fst = head, slw = head, initHead = head;
    while (slw && slw.next && fst && fst.next && fst.next.next) {
        slw = slw.next;
        fst = fst.next.next;
        // fst 和 slw 在相遇点相遇
        if (slw === fst) {
            while (slw !== initHead) {
                slw = slw.next;
                initHead = initHead.next;
            }
            return slw;
        }
    }
    return null;
};
```
## 思路

这道题和上一道题思路一致，使用快慢指针，如果俩指针会相遇，则表明有环路，同时获得相遇点。之后易证明相遇点回到合并初始点的路径长度等于非环路部分的长度，因此使用同样速度的指针，一个从相遇点出发，另外一个从初始结点出发，碰头时即为合并结点。
