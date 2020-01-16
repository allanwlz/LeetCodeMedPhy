# 合并两个有序链表
## 题目
将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。

示例：
```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
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
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var mergeTwoLists = function(l1, l2) {
    // 先用任意值初始化一个链表节点（后续只要取其下一个节点即可！）
    let mergedList = new ListNode(0);
    let initialMergedList = mergedList;
    while (l1 || l2) {
        if (!l1) { // l1 null and l2 not null
            mergedList.next = new ListNode(l2.val);
            l2 = l2.next;
        } else if (!l2) {  // l2 null and l1 not null
            mergedList.next = new ListNode(l1.val);
            l1 = l1.next;
        } else {  // l1 and l2 both not null
            if (l1.val < l2.val) {
                mergedList.next = new ListNode(l1.val);
                l1 = l1.next;
            } else {
                mergedList.next = new ListNode(l2.val);
                l2 = l2.next;
            }
        }
        mergedList = mergedList.next;
    }
    return initialMergedList.next;
};
```
## 思路
题目本身很简单，是归并排序中的有序子数组合并的过程。唯一需要注意的是在链表上进行操作。
