# 合并K个排序链表
## 题目
合并 ``k`` 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。

**示例:**
```
输入:
[
  1->4->5,
  1->3->4,
  2->6
]
输出: 1->1->2->3->4->4->5->6
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
 * @param {ListNode[]} lists
 * @return {ListNode}
 */
let mergeKLists = function(lists) {
    // 创建一个小顶堆
    // 新的堆构造函数接受一个getPrior(parentNode, childNode)函数，该函数接受父子结点两个参数并返回一个更适合当父结点的结点
    let minPriorityQueue = new PriorityQueue((a, b) => {return b.val < a.val ? b : a});
    // 首先将所有链表的首部推入小顶堆
    for (let i = 0; i < lists.length; i++) {
        let node = lists[i];
        if (node) {
            minPriorityQueue.insert(node);
        }
    }
    let sortedNode = new ListNode(0);
    let initNode = sortedNode;
    let minNode;
    while(minPriorityQueue.getSize()) {
        minNode = minPriorityQueue.delTop();
        sortedNode.next = new ListNode(minNode.val);
        if (minNode.next) {
            minPriorityQueue.insert(minNode.next);
        }
        sortedNode = sortedNode.next;
    }
    return initNode.next;
};
// 省略PriorityQueue构造函数部分
```

## 思路
在求解之前，首先讲解一下思路吧：

