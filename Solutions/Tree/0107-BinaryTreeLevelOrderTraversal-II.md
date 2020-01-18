# 二叉树的层次遍历II
## 题目
给定一个二叉树，返回其节点值自底向上的层次遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

**例如：**
```
给定二叉树 [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
```

返回其自底向上的层次遍历为：
```
[
  [15,7],
  [9,20],
  [3]
]
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
 * @param {TreeNode} root
 * @return {number[][]}
 */
let levelOrderBottom = function(root) {
    // 针对空的情况
    if (!root) {
        return [];
    } else {
        // 结果
        let result = [];
        // 辅助队列
        let treeNodeQueue = [];
        treeNodeQueue.push(root);
        root.depth = 0;
        while (treeNodeQueue.length) {
            let node = treeNodeQueue.shift();
            if (node.left) {
                node.left.depth = node.depth + 1;
                treeNodeQueue.push(node.left);
            }
            if (node.right) {
                node.right.depth = node.depth + 1;
                treeNodeQueue.push(node.right);
            }
            if (result[node.depth]) {
                result[node.depth].push(node.val);
            } else {
                result[node.depth] = [node.val];
            }
        }
        return result.reverse();
    }
};
```

## 思路
首先回顾下层次遍历，层次遍历的迭代形式代码《数据结构（C++语言版）》为：
```C++
template <typename T> template <typename VST>
void BinNode<T>::travLevel (VST & visit) {
    Queue<BinNodePosi(T)> Q;
    Q.enqueue(this);
    while (!Q.empty()) {
        BinNodePosi(T) x = Q.dequeue();
        visit(x -> data);
        if (hasLeftChild(*x)) Q.enqueue(x -> leftChild);
        if (hasRightChild(*x)) Q.enqueue(x -> rightChild);
    }
}
```

我的解法实际上是在此基础上稍稍进行了修改，在每次访问的过程中，会记录一次当前结点的层数，然后其左右子结点的层数在其父节点加一，然后访问``val``值的过程中按照结点的层数将数据给到对应的子数组中去。
