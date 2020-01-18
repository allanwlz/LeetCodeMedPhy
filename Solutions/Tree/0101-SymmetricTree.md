# 对称二叉树
## 题目
给定一个二叉树，检查它是否镜像对称。

例如，二叉树 ``[1, 2, 2, 3, 4, 4, 3]`` 是对称的。

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

但是下面这个 ``[1,2,2,null,3,null,3]`` 则不是镜像对称的:

```
    1
   / \
  2   2
   \   \
   3    3
```

**说明:**

如果你可以运用递归和迭代两种方法解决这个问题，会很加分。

## 解法
解答本题的思路是：给出根节点后（首先需要判断根节点是否同时具有左右子树，否则返回false），之后使用两个指针进行镜像地访问，每次访问得到结果后判断值是否相同。

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
var isSymmetric = function(root) {
    // 空树认为是镜像对称的
    if (!root) {
        return true;
    }
    return symmetricWalk(root.left, root.right);
};

// 镜像地访问两棵树
function symmetricWalk (leftRoot, rightRoot) {
    // 同时为空
    if (!leftRoot && !rightRoot) {
        return true;
    } else if (!leftRoot || !rightRoot) {
        return false;
    } else {
        if (leftRoot.val !== rightRoot.val) {
            return false;
        } else {
            return symmetricWalk(leftRoot.left, rightRoot.right) && symmetricWalk(leftRoot.right, rightRoot.left);
        }
    }
}
```

## 思路
树遍历的递归解法比较好写，但是迭代写法相对较为复杂，以后研究~
