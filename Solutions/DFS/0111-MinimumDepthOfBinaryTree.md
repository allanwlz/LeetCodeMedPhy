# 二叉树的最小深度

## 题目
给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

**说明**: 叶子节点是指没有子节点的节点。

**示例**:

给定二叉树 ``[3,9,20,null,null,15,7]``,

```
    3
   / \
  9  20
    /  \
   15   7
```
返回它的最小深度  2.

## 解法

该题的解决方法如下：

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
var minDepth = function(root) {
    if (!root) {
        return 0;
    }
    let minDepth = Infinity;

    function isLeafNode (treeNode) {
        return treeNode && treeNode.left === null && treeNode.right === null;
    }

    function traverse (treeNode, depth) {
        if (isLeafNode(treeNode)) {
            if (depth < minDepth) {
                minDepth = depth;
            }
        }
        if (treeNode.left !== null) {
            traverse(treeNode.left, depth + 1);
        }
        if (treeNode.right !== null) {
            traverse(treeNode.right, depth + 1);
        }
    }
    traverse(root, 1);
    return minDepth;
};
```

## 思路

解决这道题目的思路是，通过深度优先搜索（先序遍历）不断递归进行搜索，每次搜索到叶子节点的时候，记录当前的深度，和之前记录的深度对比，如果此深度小于之前记录的最小深度，则替换，当遍历完整棵树之后，即可得到最小深度。