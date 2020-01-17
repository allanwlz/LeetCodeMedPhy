# 链表的中间节点
## 题目
给定一个带有头结点 head 的非空单链表，返回链表的中间结点。

如果有两个中间结点，则返回第二个中间结点。

**示例 1：**
```
输入：[1,2,3,4,5]
输出：此列表中的结点 3 (序列化形式：[3,4,5])
返回的结点值为 3 。 (测评系统对该结点序列化表述是 [3,4,5])。
注意，我们返回了一个 ListNode 类型的对象 ans，这样：
ans.val = 3, ans.next.val = 4, ans.next.next.val = 5, 以及 ans.next.next.next = NULL.
```

**示例 2：**
```
输入：[1,2,3,4,5,6]
输出：此列表中的结点 4 (序列化形式：[4,5,6])
由于该列表有两个中间结点，值分别为 3 和 4，我们返回第二个结点。
```

**提示：**
- 给定链表的结点数介于 1 和 100 之间。

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
var middleNode = function(head) {
    // 先获得当前链表的长度，然后返回第 Math.floor(len / 2) + 1 个元素
    let midLen = Math.floor(getLinkedListLen(head) / 2) + 1;
    while (--midLen) {
        head = head.next;
    }
    return head;
};

// 遍历链表获得其长度
function getLinkedListLen (head) {
    let len = 0;
    while (head) {
        len ++;
        head = head.next;
    }
    return len;
}
```
## 思路
思路很简单，首先遍历链表获得其长度，之后再返回其中间位置返回。
