# 相同的树
## 题目
给定两个二叉树，编写一个函数来检验它们是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

**示例 1:**
```
输入:       1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

输出: true
```

**示例 2:**
```
输入:      1          1
          /           \
         2             2

        [1,2],     [1,null,2]

输出: false
```

**示例 3:**
```
输入:       1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]

输出: false
```
## 解法
```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {boolean}
 */
var isSameTree = function(p, q) {
    if (!p && !q) {  // 两者同为null
        return true;
    } else if (!p || !q) {  // 其中只一个为null
        return false;
    } else {
        // 对二叉树进行先序遍历
        if (p.val !== q.val) {
            return false;
        }
        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
};
```

## 思路
采用递归形式对二叉树进行先序（中序，后序）遍历，访问值出现不同时返回``false``。