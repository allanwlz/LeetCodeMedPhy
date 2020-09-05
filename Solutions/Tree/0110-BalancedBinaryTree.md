# 平衡二叉树

## 题目
给定一个二叉树，判断它是否是高度平衡的二叉树。

高度平衡二叉树定义为：*一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过1。*

**示例**:

给定二叉树 ``[3,9,20,null,null,15,7]``
```
    3
   / \
  9  20
    /  \
   15   7
```
返回 ``true``

给定二叉树 ``[1,2,2,3,3,null,null,4,4]``
```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
```
返回 ``false``
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
 * @return {boolean}
 */
var isBalanced = function(root) {
    if (!root) {
        return true;
    }
    return Math.abs(getHeight(root.left) - getHeight(root.right)) <= 1 &&
        isBalanced(root.left) &&
        isBalanced(root.right);
};

function getHeight (treeNode) {
    if (!treeNode) {
        return 0;
    }
    const leftHeight = getHeight(treeNode.left);
    const rightHeight = getHeight(treeNode.right);
    return Math.max(leftHeight, rightHeight) + 1;
}
```
## 思路

使用递归计算高度，并且判断是否平衡，但是这种做法的时间复杂度为 ``O(n^2)``，空间复杂度为 ``O(n)``。
