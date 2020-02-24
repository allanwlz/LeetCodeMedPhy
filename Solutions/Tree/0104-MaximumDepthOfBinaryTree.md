# 二叉树的最大深度
## 题目
给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。

**示例：** 给定二叉树 ``[3,9,20,null,null,15,7]``
```
    3
   / \
  9  20
    /  \
   15   7
```
返回它的最大深度 3 。

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
 * @param {TreeNode} root
 * @return {number}
 */
var maxDepth = function(root) {
    function digIntoTree(node, depth) {
        if (node) {
            // 闭包
            if (depth > maxDepth) {
                maxDepth = depth;
            }
            digIntoTree(node.left, depth + 1);
            digIntoTree(node.right, depth + 1);
        }
    }
    let maxDepth = 0;
    digIntoTree(root, 1);
    return maxDepth;
};
```
## 思路
非常简单，对二叉树递归地进行深度优先搜索，并通过 ``maxDepth`` 记录搜索到的最深的深度，返回 ``maxDepth`` 即可。